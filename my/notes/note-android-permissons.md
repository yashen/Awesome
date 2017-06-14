# 权限

- 在运行时请求权限

    <https://developer.android.com/training/permissions/requesting.html>

    从 Android 6.0（API 级别 23）开始，用户开始在应用运行时向其授予权限，而不是在应用安装时授予

- - 系统权限分为两类：[正常权限](https://developer.android.com/guide/topics/permissions/normal-permissions.html)和危险权限
- - 正常权限自动授予
- - 危险权限需要运行时发请求


检查权限

```
ContextCompat.checkSelfPermission(thisActivity,
                Manifest.permission.READ_CONTACTS)
        != PackageManager.PERMISSION_GRANTED
```
请求权限

```
ActivityCompat.requestPermissions(thisActivity,
                new String[]{Manifest.permission.READ_CONTACTS},
                requestCode)
```

处理请求结果

```

onRequestPermissionsResult(int requestCode,
        String permissions[], int[] grantResults)

```   
判断grantResult是否等于PackageManager.PERMISSION_GRANT或PackageManager.PERMISSION_DENIED



## 使用EasyPermissions

EasyPermissions可以简化上面的判断

定义发出请求和回调的方法

```
    @AfterPermissionGranted(ReuqestCode_ScanServerUrl)
    private void scanSeverUrl() {
        String[] perms = {Manifest.permission.CAMERA};
        if(EasyPermissions.hasPermissions(this,perms)){
            Intent intent = new Intent(this, ScanServerUrlActivity.class);
            startActivityForResult(intent, ReuqestCode_ScanServerUrl);
        }else{
            EasyPermissions.requestPermissions(this,"二维码扫描服务需要得到授权",ReuqestCode_ScanServerUrl,perms);
        }
    }

```


接收权限的结果

```
    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {

        super.onRequestPermissionsResult(requestCode,permissions,grantResults);

        EasyPermissions.onRequestPermissionsResult(requestCode,permissions,grantResults,this);

    }

```

如果需要在不能得到授权的时候做点什么，实现接口EasyPermissions.PermissionCallbacks

```

    @Override
    public void onPermissionsGranted(int requestCode, List<String> perms) {

    }

    @Override
    public void onPermissionsDenied(int requestCode, List<String> perms) {
        Toast.makeText(this,"请求授权失败",Toast.LENGTH_LONG).show();
    }

```



