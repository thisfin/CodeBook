# NSTextView

## 中英文混排固定行高

新建一个类实现 NSATSTypesetter

```
import Cocoa

class WYTypesetter: NSATSTypesetter {
    override func willSetLineFragmentRect(_ lineRect: UnsafeMutablePointer<NSRect>, forGlyphRange glyphRange: NSRange, usedRect: UnsafeMutablePointer<NSRect>, baselineOffset: UnsafeMutablePointer<CGFloat>) {
        let font = NSFont.userFixedPitchFont(ofSize: Constants.hostInfoFontSize)
        let lineHeight = layoutManager?.defaultLineHeight(for: font!)

        lineRect.pointee.size.height = lineHeight!
        usedRect.pointee.size.height = lineHeight!
        baselineOffset.pointee = (layoutManager?.defaultBaselineOffset(for: font!))!
    }
}
```

在 NSTextView 中设置

```
textView.layoutManager?.typesetter = WYTypesetter()
```

---

## 响应拷贝粘贴等快捷键操作

建立 NSTextView 的扩展

```
import Cocoa

extension NSTextView {
    override open func performKeyEquivalent(with event: NSEvent) -> Bool {
        if event.type == .keyDown {
            switch event.modifierFlags.rawValue & NSEventModifierFlags.deviceIndependentFlagsMask.rawValue {
            case NSEventModifierFlags.command.rawValue:
                switch event.charactersIgnoringModifiers! {
                case "x":
                    if NSApp.sendAction(#selector(NSText.cut(_:)), to: nil, from: self) {
                        return true
                    }
                case "c":
                    if NSApp.sendAction(#selector(NSText.copy(_:)), to: nil, from: self) {
                        return true
                    }
                case "v":
                    if NSApp.sendAction(#selector(NSText.paste(_:)), to: nil, from: self) {
                        return true
                    }
                case "z":
                    if NSApp.sendAction(Selector(("undo:")), to: nil, from: self) {
                        return true
                    }
                case "a":
                    if NSApp.sendAction(#selector(NSText.selectAll(_:)), to: nil, from: self) {
                        return true
                    }
                default:
                    ()
                }
            case NSEventModifierFlags.command.rawValue | NSEventModifierFlags.shift.rawValue:
                if event.charactersIgnoringModifiers == "Z" {
                    if NSApp.sendAction(Selector(("redo:")), to:nil, from:self) {
                        return true
                    }
                }
            default:
                ()
            }
        }
        return super.performKeyEquivalent(with: event)
    }
}
```
