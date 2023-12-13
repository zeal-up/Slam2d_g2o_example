# g2o example —— tutorial_slam2d

## Different from the original example

1. 原始例子作为g2o项目的一部分直接编译，这里将其单独拿出来作为单独例子编译
2. 原始例子由于使用自定义数据类型，因此保存下来的`.g2o`文件无法直接用`g2o_viewer`可视化。因此，添加一个子文件夹`tutorial_builtin_types`，将例子中使用到的数据类型改为g2o内置的数据类型，这样保存下来的`.g2o`文件就可以用`g2o_viewer`可视化了。