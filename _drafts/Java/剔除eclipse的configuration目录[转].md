
eclipse 3.4以前的版本，如果出现什么问题了，一般都会选择删除eclipse安装目录下configuration目录下除了config.ini之外的所有文件，同时在删除eclipse工作空间中的.metadata目录，这样就删除掉了eclipse的所有的配置信息，重新得到了一个类似全新安装的eclipse了，通常这种方法能够解决很多eclipse中遇到的错误。
但是，eclipse 3.4 情况就不一样了，一个全新的eclipse/configuration目录下不再是只有一个config.ini文件，另外多了三个目录:

* .setting
* org.eclipse.update
* org.eclipse.equinox.simpleconfigurator

其实这三个目录存在的原因是p2的出现，eclipse 3.4 全新推出的更新管理器，如果我们想清空eclipse的配置信息，需要保留configuration目录下的config.ini和org.eclipse.equinox.simpleconfigurator目录，注意，只需要保留这两个目录。
如果是删除了eclipse的整个configuration目录后，eclipse无法启动，也不用怕。
由于equinox可以创建 configuration目录，但是无法自己创建config.ini文件。在启动eclipse的时候，需要用到config.ini中的配置内容。 
删除了configuration后，启动eclipse会自动重建configuration目录。
然后可以自己在configuration目录下新建一个config.ini文件，增加以下五行内容到config.ini文件中。

```
osgi.splashpath = platform:/base/plugins/org.eclipse.platform
osgi.bundles=org.eclipse.equinox.common@2:start, org.eclipse.update.configurator@3:start, org.eclipse.core.runtime@start
eclipse.product=org.eclipse.sdk.ide
osgi.instance.area.default=@user.home/workspace
eof=eof
```

保存文件后，重新启动eclipse就没有问题了。

注：3.4.1的原版为：

```
#this configuration file was written by: org.eclipse.equinox.internal.frameworkadmin.equinox.equinoxfwconfigfileparser
#thu sep 11 19:36:01 edt 2008
org.eclipse.update.reconcile=false
osgi.launcherpath=.
eclipse.p2.profile=sdkprofile
osgi.instance.area.default=@user.home/workspace
osgi.framework=file\:plugins/org.eclipse.osgi_3.4.2.r34x_v20080826-1230.jar
eclipse.buildid=m20080911-1700
osgi.bundles=reference\:file\:org.eclipse.equinox.simpleconfigurator_1.0.0.v20080604.jar@1\:start
org.eclipse.equinox.simpleconfigurator.configurl=file\:org.eclipse.equinox.simpleconfigurator/bundles.info
eclipse.product=org.eclipse.sdk.ide
osgi.splashpath=platform\:/base/plugins/org.eclipse.platform
osgi.launcherini=eclipse
eclipse.p2.data.area=@config.dir/../p2
osgi.bundles.defaultstartlevel=4
```