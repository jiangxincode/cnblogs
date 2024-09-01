# Java Swing TreeTable样例指导

如何在Java中使用TreeTable本身就是一个主题。在各种GUI库中，我们一般都是假设这种组件是现成的。但是很不幸，在Java Swing这个GUI框架中并没有一个现成的TreeTable控件。但是我们仍然可以创建一个自定义控件，来模拟TreeTable。在接下来的教程中，我们使用一个样例来说明如何做到这一点。

在Oracle的网站上（之前是Sun的网站），Philip Milne曾经写过的一个教我们如何创建一个TreeTable控件的样例教程。很可能是因为这些代码太过于老旧的缘故，我们会感觉到源码中包含了一些现在来看并不需要的"hacks"。除此之外，这个样例中内置了很多功能，这些功能掩盖了TreeTable的本质特征。为了让样例代码更容易理解，我删除了一些非必要代码，方便大家理解，同时尽量展现出TreeTable组件的本质。

下面两张图是样例完成后的效果截图，其中一个在Windows平台，另一个在Windows平台。

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/2023010723031.png)

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/2023010723032.png)

下面的示意图展示了TreeTable的类结构。基于这个示意图，我们会用后面的一些图例详细解释TreeTable是如何进行组织的。所有来自于JDK的类都用渐变色背景，新建的类则使用纯色背景，同时这些新建的类都是以'My'开头的。

![](https://raw.githubusercontent.com/jiangxincode/PicGo/master/2023010723033.png)

首先，我们创建一个`MyTreeTableModel`接口，该接口继承于`TreeModel`接口。通过扩展我们可以让一个节点拥有多个列元素。使用的时候我们一般这样声明：`TreeModel MyTreeTableModel`

```java
package de.hameister.treetable;
 
import javax.swing.tree.TreeModel;
 
public interface MyTreeTableModel extends TreeModel {
 
 
    /**
     * Returns the number of available columns.
     * @return Number of Columns
     */
    public int getColumnCount();
 
    /**
     * Returns the column name.
     * @param column Column number
     * @return Column name
     */
    public String getColumnName(int column);
 
 
    /**
     * Returns the type (class) of a column.
     * @param column Column number
     * @return Class
     */
    public Class<?> getColumnClass(int column);
 
    /**
     * Returns the value of a node in a column.
     * @param node Node
     * @param column Column number
     * @return Value of the node in the column
     */
    public Object getValueAt(Object node, int column);
 
 
    /**
     * Check if a cell of a node in one column is editable.
     * @param node Node
     * @param column Column number
     * @return true/false
     */
    public boolean isCellEditable(Object node, int column);
 
    /**
     * Sets a value for a node in one column.
     * @param aValue New value
     * @param node Node
     * @param column Column number
     */
    public void setValueAt(Object aValue, Object node, int column);
}
```

接下来，我们创建一个抽象类`MyAbstractTreeTableModel`来继承`MyTreeTableModel`。在该类中，我们保存根节点，同时提供一个方法来检查是否存在子节点，并且该类还负责管理所有的`EventListener`。`EventListener`可以确保当数据模型结构发生变化时会传递到树状结构，并被正确的显示。使用的时候我们一般这样声明：`MyTreeTableModel MyAbstractTreeTableModel`

```java
package de.hameister.treetable;
 
import javax.swing.event.EventListenerList;
import javax.swing.event.TreeModelEvent;
import javax.swing.event.TreeModelListener;
import javax.swing.tree.TreePath;
 
public abstract class MyAbstractTreeTableModel implements MyTreeTableModel {
    protected Object root;
    protected EventListenerList listenerList = new EventListenerList();
 
    private static final int CHANGED = 0;
    private static final int INSERTED = 1;
    private static final int REMOVED = 2;
    private static final int STRUCTURE_CHANGED = 3;
 
    public MyAbstractTreeTableModel(Object root) {
        this.root = root;
    }
 
    public Object getRoot() {
        return root;
    }
 
    public boolean isLeaf(Object node) {
        return getChildCount(node) == 0;
    }
 
    public void valueForPathChanged(TreePath path, Object newValue) {
    }
 
    /**
     * Die Methode wird normalerweise nicht aufgerufen.
     */
    public int getIndexOfChild(Object parent, Object child) {
        return 0;
    }
 
    public void addTreeModelListener(TreeModelListener l) {
        listenerList.add(TreeModelListener.class, l);
    }
 
    public void removeTreeModelListener(TreeModelListener l) {
        listenerList.remove(TreeModelListener.class, l);
    }
 
    private void fireTreeNode(int changeType, Object source, Object[] path, int[] childIndices, Object[] children) {
        Object[] listeners = listenerList.getListenerList();
        TreeModelEvent e = new TreeModelEvent(source, path, childIndices, children);
        for (int i = listeners.length - 2; i >= 0; i -= 2) {
            if (listeners[i] == TreeModelListener.class) {
 
                switch (changeType) {
                case CHANGED:
                    ((TreeModelListener) listeners[i + 1]).treeNodesChanged(e);
                    break;
                case INSERTED:
                    ((TreeModelListener) listeners[i + 1]).treeNodesInserted(e);
                    break;
                case REMOVED:
                    ((TreeModelListener) listeners[i + 1]).treeNodesRemoved(e);
                    break;
                case STRUCTURE_CHANGED:
                    ((TreeModelListener) listeners[i + 1]).treeStructureChanged(e);
                    break;
                default:
                    break;
                }
 
            }
        }
    }
 
    protected void fireTreeNodesChanged(Object source, Object[] path, int[] childIndices, Object[] children) {
        fireTreeNode(CHANGED, source, path, childIndices, children);
    }
 
    protected void fireTreeNodesInserted(Object source, Object[] path, int[] childIndices, Object[] children) {
        fireTreeNode(INSERTED, source, path, childIndices, children);
    }
 
    protected void fireTreeNodesRemoved(Object source, Object[] path, int[] childIndices, Object[] children) {
        fireTreeNode(REMOVED, source, path, childIndices, children);
    }
 
    protected void fireTreeStructureChanged(Object source, Object[] path, int[] childIndices, Object[] children) {
        fireTreeNode(STRUCTURE_CHANGED, source, path, childIndices, children);
    }
 
}
```

下面的类定义了视图的具体数据模型。意味着该类定义了每个数据列，以及它们对应的数据类型。同时该类还实现了接口中尚未被实现的方法。

```java
package de.hameister.treetable;
 
import java.util.Date;
 
public class MyDataModel extends MyAbstractTreeTableModel {
    // Spalten Name.
    static protected String[] columnNames = { "Knotentext", "String", "Datum", "Integer" };
 
    // Spalten Typen.
    static protected Class<?>[] columnTypes = { MyTreeTableModel.class, String.class, Date.class, Integer.class };
 
    public MyDataModel(MyDataNode rootNode) {
        super(rootNode);
        root = rootNode;
    }
 
    public Object getChild(Object parent, int index) {
        return ((MyDataNode) parent).getChildren().get(index);
    }
 
 
    public int getChildCount(Object parent) {
        return ((MyDataNode) parent).getChildren().size();
    }
 
 
    public int getColumnCount() {
        return columnNames.length;
    }
 
 
    public String getColumnName(int column) {
        return columnNames[column];
    }
 
 
    public Class<?> getColumnClass(int column) {
        return columnTypes[column];
    }
 
    public Object getValueAt(Object node, int column) {
        switch (column) {
        case 0:
            return ((MyDataNode) node).getName();
        case 1:
            return ((MyDataNode) node).getCapital();
        case 2:
            return ((MyDataNode) node).getDeclared();
        case 3:
            return ((MyDataNode) node).getArea();
        default:
            break;
        }
        return null;
    }
 
    public boolean isCellEditable(Object node, int column) {
        return true; // Important to activate TreeExpandListener
    }
 
    public void setValueAt(Object aValue, Object node, int column) {
    }
 
}
```

下面的类是一个简单的值对象，通过一些get/set方法保存数据节点。

```java
package de.hameister.treetable;
 
import java.util.Collections;
import java.util.Date;
import java.util.List;
 
public class MyDataNode {
 
    private String name;
    private String capital;
    private Date declared;
    private Integer area;
 
    private List<MyDataNode> children;
 
    public MyDataNode(String name, String capital, Date declared, Integer area, List<MyDataNode> children) {
        this.name = name;
        this.capital = capital;
        this.declared = declared;
        this.area = area;
        this.children = children;
 
        if (this.children == null) {
            this.children = Collections.emptyList();
        }
    }
 
    public String getName() {
        return name;
    }
 
    public String getCapital() {
        return capital;
    }
 
    public Date getDeclared() {
        return declared;
    }
 
    public Integer getArea() {
        return area;
    }
 
    public List<MyDataNode> getChildren() {
        return children;
    }
 
    /**
     * Knotentext vom JTree.
     */
    public String toString() {
        return name;
    }
}
```

到此为止，数据模型部分已经准备完毕。在main方法所在的类中，我们可以创建包含节点的数据模型了。负责呈现界面的类将会在后面进行描述。在实际是使用过程中，数据结构不会在开始就通过一个方法就完整的创建出来，大部分场景下是需要在运行过程中通过数据库获取这些数据。

```java
package de.hameister.treetable;
 
import java.awt.Container;
import java.awt.GridLayout;
import java.util.ArrayList;
import java.util.Date;
import java.util.List;
 
import javax.swing.JFrame;
import javax.swing.JScrollPane;
import javax.swing.SwingUtilities;
import javax.swing.UIManager;
 
public class TreeTableMain extends JFrame {
 
 
    public TreeTableMain() {
        super("Tree Table Demo");
 
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
 
        setLayout(new GridLayout(0, 1));
 
        MyAbstractTreeTableModel treeTableModel = new MyDataModel(createDataStructure());
 
        MyTreeTable myTreeTable = new MyTreeTable(treeTableModel);
 
        Container cPane = getContentPane();
 
        cPane.add(new JScrollPane(myTreeTable));
 
        setSize(1000, 800);
        setLocationRelativeTo(null);
 
 
    }
 
 
    private static MyDataNode createDataStructure() {
        List<MyDataNode> children1 = new ArrayList<MyDataNode>();
        children1.add(new MyDataNode("N12", "C12", new Date(), Integer.valueOf(50), null));
        children1.add(new MyDataNode("N13", "C13", new Date(), Integer.valueOf(60), null));
        children1.add(new MyDataNode("N14", "C14", new Date(), Integer.valueOf(70), null));
        children1.add(new MyDataNode("N15", "C15", new Date(), Integer.valueOf(80), null));
 
        List<MyDataNode> children2 = new ArrayList<MyDataNode>();
        children2.add(new MyDataNode("N12", "C12", new Date(), Integer.valueOf(10), null));
        children2.add(new MyDataNode("N13", "C13", new Date(), Integer.valueOf(20), children1));
        children2.add(new MyDataNode("N14", "C14", new Date(), Integer.valueOf(30), null));
        children2.add(new MyDataNode("N15", "C15", new Date(), Integer.valueOf(40), null));
 
        List<MyDataNode> rootNodes = new ArrayList<MyDataNode>();
        rootNodes.add(new MyDataNode("N1", "C1", new Date(), Integer.valueOf(10), children2));
        rootNodes.add(new MyDataNode("N2", "C2", new Date(), Integer.valueOf(10), children1));
        rootNodes.add(new MyDataNode("N3", "C3", new Date(), Integer.valueOf(10), children2));
        rootNodes.add(new MyDataNode("N4", "C4", new Date(), Integer.valueOf(10), children1));
        rootNodes.add(new MyDataNode("N5", "C5", new Date(), Integer.valueOf(10), children1));
        rootNodes.add(new MyDataNode("N6", "C6", new Date(), Integer.valueOf(10), children1));
        rootNodes.add(new MyDataNode("N7", "C7", new Date(), Integer.valueOf(10), children1));
        rootNodes.add(new MyDataNode("N8", "C8", new Date(), Integer.valueOf(10), children1));
        rootNodes.add(new MyDataNode("N9", "C9", new Date(), Integer.valueOf(10), children1));
        rootNodes.add(new MyDataNode("N10", "C10", new Date(), Integer.valueOf(10), children1));
        rootNodes.add(new MyDataNode("N11", "C11", new Date(), Integer.valueOf(10), children1));
        rootNodes.add(new MyDataNode("N12", "C7", new Date(), Integer.valueOf(10), children1));
        rootNodes.add(new MyDataNode("N13", "C8", new Date(), Integer.valueOf(10), children1));
        rootNodes.add(new MyDataNode("N14", "C9", new Date(), Integer.valueOf(10), children1));
        rootNodes.add(new MyDataNode("N15", "C10", new Date(), Integer.valueOf(10), children1));
        rootNodes.add(new MyDataNode("N16", "C11", new Date(), Integer.valueOf(10), children1));
        MyDataNode root = new MyDataNode("R1", "R1", new Date(), Integer.valueOf(10), rootNodes);
 
        return root;
    }
 
    public static void main(final String[] args) {
        Runnable gui = new Runnable() {
 
            public void run() {
                try {
                    UIManager.setLookAndFeel(UIManager.getSystemLookAndFeelClassName());
                } catch (Exception e) {
                    e.printStackTrace();
                }
                new TreeTableMain().setVisible(true);
            }
        };
        SwingUtilities.invokeLater(gui);
    }
}
```

因为TreeTable组件是由JTree组件和JTable组件组合而成，
Since the TreeTable is composed of a JTree component and a JTable component, it must be ensured that a continuous row is always marked when selecting the tree or table. To ensure this, create a class that extends the DefaultTreeSelectionModel. This SelectionModel is later assigned to the JTree and the JTable. MyTreeTableSelectionModel

```java
package de.hameister.treetable;
 
import javax.swing.ListSelectionModel;
import javax.swing.event.ListSelectionEvent;
import javax.swing.event.ListSelectionListener;
import javax.swing.tree.DefaultTreeSelectionModel;
 
public class MyTreeTableSelectionModel extends DefaultTreeSelectionModel {
 
    public MyTreeTableSelectionModel() {
        super();
 
        getListSelectionModel().addListSelectionListener(new ListSelectionListener() {
            @Override
            public void valueChanged(ListSelectionEvent e) {
 
            }
        });
    }
 
    ListSelectionModel getListSelectionModel() {
        return listSelectionModel;
    }
}
```

To enable the opening of the tree, you need a . That's why you create a class that extends and implements the interface. The only function of the class is to forward a double click to the tree. The method checks whether the first column () has been clicked. If this is the case, a double click is forwarded to the so that they can react. AbstractCellEditorMyTreeTableCellEditorAbstractCellEditorTableCellEditorMyTreeTableCellEditorisCellEditablecolumn1treeExpansionListener

```java
package de.hameister.treetable;
 
import java.awt.Component;
import java.awt.event.MouseEvent;
import java.util.EventObject;
 
import javax.swing.AbstractCellEditor;
import javax.swing.JTable;
import javax.swing.JTree;
import javax.swing.table.TableCellEditor;
 
public class MyTreeTableCellEditor extends AbstractCellEditor implements TableCellEditor {
 
    private JTree tree;
    private JTable table;
 
    public MyTreeTableCellEditor(JTree tree, JTable table) {
        this.tree = tree;
        this.table = table;
    }
 
    public Component getTableCellEditorComponent(JTable table, Object value, boolean isSelected, int r, int c) {
        return tree;
    }
 
    public boolean isCellEditable(EventObject e) {
        if (e instanceof MouseEvent) {
            int colunm1 = 0;
            MouseEvent me = (MouseEvent) e;
            int doubleClick = 2;
            MouseEvent newME = new MouseEvent(tree, me.getID(), me.getWhen(), me.getModifiers(), me.getX() - table.getCellRect(0, colunm1, true).x, me.getY(), doubleClick, me.isPopupTrigger());
            tree.dispatchEvent(newME);
        }
        return false;
    }
 
    @Override
    public Object getCellEditorValue() {
        return null;
    }
 
}
```

Since in Java Swing the GUI components still required a Model, which is unlike the actual data model, a class , which inherits from , is now created. This class is later used in the class as a model for the . If the TreeTable later asks for values to be displayed, it must be distinguished whether the requested values can be delivered by the tree or directly by the data model. In addition, the class is still generated and registered. This reacts to clicks in the tree and ensures that the tree is opened and closed. MyTreeTableModelAdapterAbstractTableModelMyTreeTableJTableMyAbstractTreeTableModelTreeExpansionListener

```java
package de.hameister.treetable;
 
import java.awt.Rectangle;
 
import javax.swing.JTree;
import javax.swing.event.TreeExpansionEvent;
import javax.swing.event.TreeExpansionListener;
import javax.swing.table.AbstractTableModel;
import javax.swing.tree.TreePath;
 
public class MyTreeTableModelAdapter extends AbstractTableModel {
 
     JTree tree;
    MyAbstractTreeTableModel treeTableModel;
 
    public MyTreeTableModelAdapter(MyAbstractTreeTableModel treeTableModel, JTree tree) {
        this.tree = tree;
        this.treeTableModel = treeTableModel;
 
        tree.addTreeExpansionListener(new TreeExpansionListener() {
            public void treeExpanded(TreeExpansionEvent event) {
                fireTableDataChanged();
            }
 
            public void treeCollapsed(TreeExpansionEvent event) {
                fireTableDataChanged();
            }
        });
    }
 
 
 
    public int getColumnCount() {
        return treeTableModel.getColumnCount();
    }
 
    public String getColumnName(int column) {
        return treeTableModel.getColumnName(column);
    }
 
    public Class<?> getColumnClass(int column) {
        return treeTableModel.getColumnClass(column);
    }
 
    public int getRowCount() {
        return tree.getRowCount();
    }
 
    protected Object nodeForRow(int row) {
        TreePath treePath = tree.getPathForRow(row);
        return treePath.getLastPathComponent();
    }
 
    public Object getValueAt(int row, int column) {
        return treeTableModel.getValueAt(nodeForRow(row), column);
    }
 
    public boolean isCellEditable(int row, int column) {
        return treeTableModel.isCellEditable(nodeForRow(row), column);
    }
 
    public void setValueAt(Object value, int row, int column) {
        treeTableModel.setValueAt(value, nodeForRow(row), column);
    }
}
```

Finally, the JTree and the JTable have to be created. The Tree component inherits from and implements the interface. This class ensures that the row heights of Tree and Table are the same and that the background colors are set correctly during selection. In addition, it is ensured that the elements of the tree are correctly indented depending on the level. MyTreeTableCellRendererJTreeTableCellRenderer

```java
package de.hameister.treetable;
 
import java.awt.Component;
import java.awt.Graphics;
 
import javax.swing.JTable;
import javax.swing.JTree;
import javax.swing.table.TableCellRenderer;
import javax.swing.tree.TreeModel;
 
 
public class MyTreeTableCellRenderer extends JTree implements TableCellRenderer {
    /** Die letzte Zeile, die gerendert wurde. */
    protected int visibleRow;
 
    private MyTreeTable treeTable;
 
    public MyTreeTableCellRenderer(MyTreeTable treeTable, TreeModel model) {
        super(model);
        this.treeTable = treeTable;
 
        // Setzen der Zeilenhoehe fuer die JTable
        // Muss explizit aufgerufen werden, weil treeTable noch
        // null ist, wenn super(model) setRowHeight aufruft!
        setRowHeight(getRowHeight());
    }
 
    /**
     * Tree und Table muessen die gleiche Hoehe haben.
     */
    public void setRowHeight(int rowHeight) {
        if (rowHeight > 0) {
            super.setRowHeight(rowHeight);
            if (treeTable != null && treeTable.getRowHeight() != rowHeight) {
                treeTable.setRowHeight(getRowHeight());
            }
        }
    }
 
    /**
     * Tree muss die gleiche Hoehe haben wie Table.
     */
    public void setBounds(int x, int y, int w, int h) {
        super.setBounds(x, 0, w, treeTable.getHeight());
    }
 
    /**
     * Sorgt fuer die Einrueckung der Ordner.
     */
    public void paint(Graphics g) {
        g.translate(0, -visibleRow * getRowHeight());
 
        super.paint(g);
    }
 
    /**
     * Liefert den Renderer mit der passenden Hintergrundfarbe zurueck.
     */
    public Component getTableCellRendererComponent(JTable table, Object value, boolean isSelected, boolean hasFocus, int row, int column) {
        if (isSelected)
            setBackground(table.getSelectionBackground());
        else
            setBackground(table.getBackground());
 
        visibleRow = row;
        return this;
    }
}
```

Now that the data model, the auxiliary components and the Main class are in place, the actual TreeTable is still missing. For this purpose, the class is created. This inherits from . Since multiple inheritance is not possible with Java, the Tree component is included in the class via an association. The data model is passed to both the (Tree) and the Object (Table). The class is set as a model. For the simultaneous selection of Tree and Table, this is used for Tree and Table. Then you have to set a default renderer for the tree and set a default editor for the table. MyTreeTableJTableMyTreeTableCellRendererMyAbstractTreeTableModelMyTreeTableCellRendererMyTreeTableModelAdapterMyTreeTableModelAdapterMyTreeTableSelectionModel

```java
package de.hameister.treetable;
 
import java.awt.Dimension;
 
import javax.swing.JTable;
 
public class MyTreeTable extends JTable {
 
    private MyTreeTableCellRenderer tree;
 
 
    public MyTreeTable(MyAbstractTreeTableModel treeTableModel) {
        super();
 
        // JTree erstellen.
        tree = new MyTreeTableCellRenderer(this, treeTableModel);
 
        // Modell setzen.
        super.setModel(new MyTreeTableModelAdapter(treeTableModel, tree));
 
        // Gleichzeitiges Selektieren fuer Tree und Table.
        MyTreeTableSelectionModel selectionModel = new MyTreeTableSelectionModel();
        tree.setSelectionModel(selectionModel); //For the tree
        setSelectionModel(selectionModel.getListSelectionModel()); //For the table
 
 
        // Renderer fuer den Tree.
        setDefaultRenderer(MyTreeTableModel.class, tree);
        // Editor fuer die TreeTable
        setDefaultEditor(MyTreeTableModel.class, new MyTreeTableCellEditor(tree, this));
 
        // Kein Grid anzeigen.
        setShowGrid(false);
 
        // Keine Abstaende.
        setIntercellSpacing(new Dimension(0, 0));
 
    }
}
```

If the individual classes are now compiled with , then one should have a working TreeTable component. But as already indicated above, it is not to be understood that such a component is not part of Java. I find it incredible that you have to implement 8 classes to get a really simple TreeTable. It should be noted that functionalities such as javac

edit
Connected rows and columns
Colored rows and columns
SwingWorker for long-running expansion events
Icons in the tree
Swing components in the Table (ComboBox, Images, ...)
have not yet been taken into account at all. It's easy to imagine how much source code and time would have to go into these features in order to have a working component.
