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
