# 阅读笔记 - 理解front-end framework的design pattern，以及coding standard

回顾一年多的工作经历，在工作中写了很多代码，实现了很多功能，明白JavaScript的概念和语法，会用工业界最流行的framework和工具，偶尔会造轮子写几个小的npm package，也在不断地阅读和学习新的技术。然而，逐渐逐渐地感觉遇到了技术的提高瓶颈，以及未来的危机。

自己现有的大多数知识都是围绕着framework，而这些framework最核心的技术完全没有触碰到。这么继续下去恐怕只会是lower-level的developer，而不是engineer。

最近借着准备front-end面试的机会深入地阅读了the secrests of javascript ninja这本书，才发现自己对front-end和javascript的了解实在是太过有限。

**会写几个function改变style和content，这样的工作并不需要一个engineer来完成吧？**

最近在阅读了react和redux的source code后，才理解为什么美帝的tech giant在面试front-end engineer时会对computer science fundamentals这么看中。在framework背后做支撑的全部都是cs fundamental knowledge，以及经典的pub / sub design pattern.
