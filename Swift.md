# Swift

## Objective-C Bridge

1. File -> New -> File -> Header File
1. 文件名为 `[ProjectName]-Bridging-Header.h`
1. 文件内容为 `#import <xxx/xxx.h>`
1. Targets -> Build Settings -> All -> Swift Compiler - General -> Objective-C Bridging Header
1. 内容为 `[ProjectName]/[ProjectName]-Bridging-Header.h`

---

## 单例 Singleton

```
class SingletonTest: NSObject {
    private static let selfInstance = SingletonTest()

    public static var sharedInstance: SingletonTest {
        return selfInstance
    }

    override private init() {
        super.init()
    }
}
```

简便形式
```
class SingletonTest {
    private static let sharedInstance = SingletonTest()

    private init() {
    }
}
```

---

## sandbox 访问外部文件添加 bookmark

.entitlements 文件中增加如下, 注意 user-selected 一定要是读写权限!!!, 不然 bookmark 会报错
```
    <key>com.apple.security.files.user-selected.read-write</key>
    <true/>
    <key>com.apple.security.files.bookmarks.app-scope</key>
    <true/>
```

bookmark 生成和使用的相关代码
```
    // 执行 语句封装在 block 中
    // startAccessingSecurityScopedResource 必须和 stopAccessingSecurityScopedResource 成对出现
    func handleFile(newPath: String, block: (_ url: URL) -> Void) {
        var isStale = false
        if let bookmarkData = UserDefaults.standard.object(forKey: getBookmarkKey(fileType: fileType)),
            bookmarkData is Data,
            let url = try! URL.init(resolvingBookmarkData: bookmarkData as! Data, options: .withSecurityScope, relativeTo: nil, bookmarkDataIsStale: &isStale),
            url.path == newPath {
            _ = url.startAccessingSecurityScopedResource()
            block(url)
            url.stopAccessingSecurityScopedResource()
        }
    }

    // 增加书签 一般在 OpenPanel 选择文件后调用
    func addBookmark(url: URL) {
        let bookmarkData = try! url.bookmarkData(options: .withSecurityScope, includingResourceValuesForKeys: nil, relativeTo: nil)
        UserDefaults.standard.set(bookmarkData, "key")
    }
```

---

## sandbox 访问外部文件 (也可以使用上面的方法, 固定文件的话使用这种)

.entitlements 文件中增加如下, 注意路径一定要是完成路径!!! 不要包含链接路径(例如/etc/hosts的完整路径是/private/etc/hosts)
```
    <key>com.apple.security.temporary-exception.files.absolute-path.read-write</key>
    <array>
        <string>/private/etc/hosts</string>
    </array>
```

---