# 正则表达式

## NSRegularExpression.Options
```
caseInsensitive             // 不区分字母大小写的模式
allowCommentsAndWhitespace  // 忽略掉正则表达式中的空格和#号之后的字符
ignoreMetacharacters        // 将正则表达式整体作为字符串处理
dotMatchesLineSeparators    // 允许.匹配任何字符，包括换行符
anchorsMatchLines           // 允许^和$符号匹配行的开头和结尾
useUnixLineSeparators       // 设置\n为唯一的行分隔符，否则所有的都有效。
useUnicodeWordBoundaries    // 使用Unicode TR#29标准作为词的边界，否则所有传统正则表达式的词边界都有效
```

## NSRegularExpression.MatchingOptions
```
reportProgress              // 找到最长的匹配字符串后调用block回调
reportCompletion            // 找到任何一个匹配串后都回调一次block
anchored                    // 从匹配范围的开始出进行极限匹配
withTransparentBounds       // 允许匹配的范围超出设置的范围
withoutAnchoringBounds      // 禁止^和$自动匹配行还是和结束
```

## NSRegularExpression.MatchingFlags
```
progress                    // 匹配到最长串是被设置
completed                   // 全部分配完成后被设置
hitEnd                      // 匹配到设置范围的末尾时被设置
requiredEnd                 // 当前匹配到的字符串在匹配范围的末尾时被设置
internalError               // 由于错误导致的匹配失败时被设置
```
