# 18. iOS 持续发布

Date: 20/04/2017

## Status

Accepted

## Context

目前使用测试同学的工作电脑做 iOS 的打包与分发，对测试同学有一定的影响。

## Decision

![][image-1]

基本流程不变，将打包工作交由第三方服务 buddybuild 处理并分发。
buddybuild 本可以直接分发，但由于其分发网络在国内比较慢，所以继续使用 fir.im 进行分发

## Consequences

免费版单次打包过程限制在 20 分钟内，无限次打包但会优先打包付费用的的应用，未来长期的高频次使用需要购买付费版。

Refs:

Custom Build Steps: [http://docs.buddybuild.com/docs/custom-prebuild-and-postbuild-steps][1]

[1]:	http://docs.buddybuild.com/docs/custom-prebuild-and-postbuild-steps

[image-1]:	decisions/files/Continuous-delivery-iOS.png