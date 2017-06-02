# Xcode

## 代码提示失效

执行以下命令
```
rm -rf ~/Library/Developer/Xcode/DerivedData/[project_name]  
rm -rf ~/Library/Caches/com.apple.dt.Xcode
```

---

## 查看应用的 bundle id

执行命令 (以程序Terminal为例)
```
/usr/libexec/PlistBuddy -c 'Print CFBundleIdentifier' /Applications/Utilities/Terminal.app/Contents/Info.plist
```

---

## sandbox 中执行 applescript 操作其他 app

修改 .entitlements 文件 (以 Terminal 为例, 注意 bundle id 要小写)
```
<key>com.apple.security.temporary-exception.apple-events</key>
<array>
    <string>com.apple.terminal</string>
</array>
```

---
