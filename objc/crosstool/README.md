# ObjC on GNU/Linux crosstool

## Just --crosstool_top

Build with:

```
bazel build --crosstool_top=//objc/crosstool:default-toolchain //objc:objc
```

### Error

```
ERROR: /home/ivucica/bazel-hello/objc/BUILD:1:1: in objc_library rule //objc:lib: Expected action_config for 'objc-compile' to be configured
ERROR: Analysis of target '//objc:objc' failed; build aborted: Analysis of target '//objc:lib' failed; build aborted
INFO: Elapsed time: 0.463s
FAILED: Build did NOT complete successfully (0 packages loaded)
```


## Also --apple_crosstool_top

Build with:

```
bazel build --crosstool_top=//objc/crosstool:default-toolchain --apple_crosstool_top=//objc/crosstool:default-toolchain --ios_multi_cpus=k8  //objc:objc
```

(This will no longer work as k8 definition has been removed)

### Error

```
Unhandled exception thrown during build; message: Unrecoverable error while evaluating node '//objc:lib com.google.devtools.build.lib.skyframe.BuildConfigurationValue$Key@bbc98fe2 false (1828823941)' (requested by nodes '//objc:objc com.google.devtools.build.lib.skyframe.BuildConfigurationValue$Key@766e005 false (894464277)')
INFO: Elapsed time: 1.247s
FAILED: Build did NOT complete successfully (16 packages loaded)
java.lang.RuntimeException: Unrecoverable error while evaluating node '//objc:lib com.google.devtools.build.lib.skyframe.BuildConfigurationValue$Key@bbc98fe2 false (1828823941)' (requested by nodes '//objc:objc com.google.devtools.build.lib.skyframe.BuildConfigurationValue$Key@766e005 false (894464277)')
	at com.google.devtools.build.skyframe.AbstractParallelEvaluator$Evaluate.run(AbstractParallelEvaluator.java:414)
	at com.google.devtools.build.lib.concurrent.AbstractQueueVisitor$WrappedRunnable.run(AbstractQueueVisitor.java:355)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
	at java.lang.Thread.run(Thread.java:748)
Caused by: java.lang.IllegalArgumentException: No supported apple platform registered for target cpu ios_k8
	at com.google.devtools.build.lib.rules.apple.ApplePlatform.forTargetCpu(ApplePlatform.java:218)
	at com.google.devtools.build.lib.rules.apple.ApplePlatform.forTarget(ApplePlatform.java:204)
	at com.google.devtools.build.lib.rules.apple.AppleConfiguration.getSingleArchPlatform(AppleConfiguration.java:287)
	at com.google.devtools.build.lib.rules.objc.ObjcVariablesExtension.addFrameworkVariables(ObjcVariablesExtension.java:171)
	at com.google.devtools.build.lib.rules.objc.ObjcVariablesExtension.addVariables(ObjcVariablesExtension.java:133)
	at com.google.devtools.build.lib.rules.cpp.CppModel.setupCompileBuildVariables(CppModel.java:700)
	at com.google.devtools.build.lib.rules.cpp.CppModel.createSourceAction(CppModel.java:1090)
	at com.google.devtools.build.lib.rules.cpp.CppModel.createCcCompileActions(CppModel.java:775)
	at com.google.devtools.build.lib.rules.cpp.CcLibraryHelper.compile(CcLibraryHelper.java:1043)
	at com.google.devtools.build.lib.rules.objc.CompilationSupport.compile(CompilationSupport.java:368)
	at com.google.devtools.build.lib.rules.objc.CompilationSupport.ccCompileAndLink(CompilationSupport.java:402)
	at com.google.devtools.build.lib.rules.objc.CompilationSupport.registerCompileAndArchiveActions(CompilationSupport.java:1088)
	at com.google.devtools.build.lib.rules.objc.CompilationSupport.registerCompileAndArchiveActions(CompilationSupport.java:1132)
	at com.google.devtools.build.lib.rules.objc.CompilationSupport.registerCompileAndArchiveActions(CompilationSupport.java:924)
	at com.google.devtools.build.lib.rules.objc.ObjcLibrary.create(ObjcLibrary.java:77)
	at com.google.devtools.build.lib.rules.objc.ObjcLibrary.create(ObjcLibrary.java:34)
	at com.google.devtools.build.lib.analysis.ConfiguredTargetFactory.createRule(ConfiguredTargetFactory.java:364)
	at com.google.devtools.build.lib.analysis.ConfiguredTargetFactory.createConfiguredTarget(ConfiguredTargetFactory.java:240)
	at com.google.devtools.build.lib.skyframe.SkyframeBuildView.createConfiguredTarget(SkyframeBuildView.java:517)
	at com.google.devtools.build.lib.skyframe.ConfiguredTargetFunction.createConfiguredTarget(ConfiguredTargetFunction.java:699)
	at com.google.devtools.build.lib.skyframe.ConfiguredTargetFunction.compute(ConfiguredTargetFunction.java:278)
	at com.google.devtools.build.skyframe.AbstractParallelEvaluator$Evaluate.run(AbstractParallelEvaluator.java:340)
	... 4 more
java.lang.RuntimeException: Unrecoverable error while evaluating node '//objc:lib com.google.devtools.build.lib.skyframe.BuildConfigurationValue$Key@bbc98fe2 false (1828823941)' (requested by nodes '//objc:objc com.google.devtools.build.lib.skyframe.BuildConfigurationValue$Key@766e005 false (894464277)')
	at com.google.devtools.build.skyframe.AbstractParallelEvaluator$Evaluate.run(AbstractParallelEvaluator.java:414)
	at com.google.devtools.build.lib.concurrent.AbstractQueueVisitor$WrappedRunnable.run(AbstractQueueVisitor.java:355)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
	at java.lang.Thread.run(Thread.java:748)
Caused by: java.lang.IllegalArgumentException: No supported apple platform registered for target cpu ios_k8
	at com.google.devtools.build.lib.rules.apple.ApplePlatform.forTargetCpu(ApplePlatform.java:218)
	at com.google.devtools.build.lib.rules.apple.ApplePlatform.forTarget(ApplePlatform.java:204)
	at com.google.devtools.build.lib.rules.apple.AppleConfiguration.getSingleArchPlatform(AppleConfiguration.java:287)
	at com.google.devtools.build.lib.rules.objc.ObjcVariablesExtension.addFrameworkVariables(ObjcVariablesExtension.java:171)
	at com.google.devtools.build.lib.rules.objc.ObjcVariablesExtension.addVariables(ObjcVariablesExtension.java:133)
	at com.google.devtools.build.lib.rules.cpp.CppModel.setupCompileBuildVariables(CppModel.java:700)
	at com.google.devtools.build.lib.rules.cpp.CppModel.createSourceAction(CppModel.java:1090)
	at com.google.devtools.build.lib.rules.cpp.CppModel.createCcCompileActions(CppModel.java:775)
	at com.google.devtools.build.lib.rules.cpp.CcLibraryHelper.compile(CcLibraryHelper.java:1043)
	at com.google.devtools.build.lib.rules.objc.CompilationSupport.compile(CompilationSupport.java:368)
	at com.google.devtools.build.lib.rules.objc.CompilationSupport.ccCompileAndLink(CompilationSupport.java:402)
	at com.google.devtools.build.lib.rules.objc.CompilationSupport.registerCompileAndArchiveActions(CompilationSupport.java:1088)
	at com.google.devtools.build.lib.rules.objc.CompilationSupport.registerCompileAndArchiveActions(CompilationSupport.java:1132)
	at com.google.devtools.build.lib.rules.objc.CompilationSupport.registerCompileAndArchiveActions(CompilationSupport.java:924)
	at com.google.devtools.build.lib.rules.objc.ObjcLibrary.create(ObjcLibrary.java:77)
	at com.google.devtools.build.lib.rules.objc.ObjcLibrary.create(ObjcLibrary.java:34)
	at com.google.devtools.build.lib.analysis.ConfiguredTargetFactory.createRule(ConfiguredTargetFactory.java:364)
	at com.google.devtools.build.lib.analysis.ConfiguredTargetFactory.createConfiguredTarget(ConfiguredTargetFactory.java:240)
	at com.google.devtools.build.lib.skyframe.SkyframeBuildView.createConfiguredTarget(SkyframeBuildView.java:517)
	at com.google.devtools.build.lib.skyframe.ConfiguredTargetFunction.createConfiguredTarget(ConfiguredTargetFunction.java:699)
	at com.google.devtools.build.lib.skyframe.ConfiguredTargetFunction.compute(ConfiguredTargetFunction.java:278)
	at com.google.devtools.build.skyframe.AbstractParallelEvaluator$Evaluate.run(AbstractParallelEvaluator.java:340)
	... 4 more
```

## Now ios_x86_64 and --apple_crosstool_top

Build with:

```
bazel build --crosstool_top=//objc/crosstool:default-toolchain --apple_crosstool_top=//objc/crosstool:default-toolchain --ios_multi_cpus=x86_64  //objc:objc
```

### Error

```
ERROR: /home/user/projects/bazel-hello/objc/BUILD:1:1: in objc_library rule //objc:lib: Expected action_config for 'objc-archive' to be configured
ERROR: /home/user/projects/bazel-hello/objc/BUILD:1:1: in objc_library rule //objc:lib: Expected action_config for 'c++-link-dynamic-library' to be configured
ERROR: /home/ivucica/projects/bazel-hello/objc/BUILD:1:1: in objc_library rule //objc:lib: Expected action_config for 'objc-fully-link' to be configured
ERROR: Analysis of target '//objc:objc' failed; build aborted: Analysis of target '//objc:lib' failed; build aborted
INFO: Elapsed time: 0.714s
FAILED: Build did NOT complete successfully (11 packages loaded)
```

and after defining these three

```
ERROR: Invalid toolchain configuration: multiple action configs for action 'c++-link-dynamic-library'
ERROR: Analysis of target '//objc:objc' failed; build aborted: Invalid toolchain configuration: multiple action configs for action 'c++-link-dynamic-library'
INFO: Elapsed time: 0.176s
FAILED: Build did NOT complete successfully (1 packages loaded)
```

