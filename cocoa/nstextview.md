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
