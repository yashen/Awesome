
<!-- TOC -->

- [菜单](#菜单)

<!-- /TOC -->
# 菜单

首先需要打开菜单支持

```

    @Override
    public void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setHasOptionsMenu(true);
    }

```

然后分别在onCreateOptionsMenu，onOptionsItemSelected方法里创建和处理方法



注意：菜单的处理方法会先发送到Activity的菜单处理方法里，Activity里如果没有处理才会发送到Fragment里<!-- TOC -->
