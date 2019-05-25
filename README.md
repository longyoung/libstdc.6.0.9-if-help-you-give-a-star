# 写在前面  
library not found for -libstdc++.6.0.9，今天做项目的时候碰到这个问题，解决的过程中遇到了目录路径不对的问题（不在通常的/Applications/Xcode.app......下面），花费了我半天时间，记录一下，也给别人当做参考。  

# 解决方法  
这个问题的原因是Xcode10把libstdc++换成了libc++，解决方法有2种，选择哪种都可以，能解决问题就行；但是，值得注意的是这种情况：你的项目引用了第三方库，然而这个库引用了旧库libstdc++，这时候你只能用方法2了。解决方法如下：  

方法1：  
单击项目名-->Build Phases-->Link Binary With Libraries，删除6.0.9依赖添加Libc++.tdb  
![](https://user-gold-cdn.xitu.io/2019/5/25/16aed00cd32b1b89?w=1138&h=409&f=png&s=175240)  

方法2：  
对应文件夹下添加对应的三个库，[获取Xcode9旧库](https://github.com/longyoung/libstdc.6.0.9-if-help-you-give-a-star.git)（有用给个star）  
①在RuntimeRoot的lib里面增加libstdc++.6.0.9.dylib，libstdc++.6.dylib，libstdc++.dylib  
>/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/Library/CoreSimulator/Profiles/Runtimes/iOS.simruntime/Contents/Resources/RuntimeRoot/usr/lib/（下文有进入目录方法）  

②在iPhoneOS.sdk的lib里面增加libstdc++.6.0.9.tbd，libstdc++.6.tbd，libstdc++.tbd  
>/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/usr/lib/  

③在iPhoneSimulator.sdk的lib里面增加libstdc++.6.0.9.tbd，libstdc++.6.tbd，libstdc++.tbd  
>/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneSimulator.platform/Developer/SDKs/iPhoneSimulator.sdk/usr/lib/  

# 如何进入目录  
访达-->前往文件夹...-->输入路径。（找不到目录继续往下看）  
![](https://user-gold-cdn.xitu.io/2019/5/25/16aed00cd2f09d68?w=467&h=442&f=jpeg&s=37231)
![](https://user-gold-cdn.xitu.io/2019/5/25/16aed00cd3066e2c?w=429&h=182&f=jpeg&s=7805)

# 问题中的问题
有没有小伙伴和我一样进不去目录的？把路径复制上去，进不了，什么情况？我猜测是不是我Xcode的安装路径不一样导致的？我使用mac系统的时间不是很长，不是太了解是怎么回事，后来在网上找到了查看安装路径的方法。活动监视器-->Xcode-->左上角第二个按钮-->打开的文件和端口。对比着把头替换掉就可以了。（找不到活动监视器的往下看，否则忽略）  
>/Users/feiwei/Downloads/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/Library/CoreSimulator/Profiles/Runtimes/iOS.simruntime/Contents/Resources/RuntimeRoot/usr/lib/
![](https://user-gold-cdn.xitu.io/2019/5/25/16aed00cd317ed47?w=1240&h=557&f=png&s=438968)

# 活动监视器
这个步骤是写给不怎么会用mac的小伙伴的，有可能不在「其他」这个归类里面，在Launchpad里面找就行，你一定能找到的。上图：  
![](https://user-gold-cdn.xitu.io/2019/5/25/16aed00cd31d233b?w=118&h=122&f=png&s=17623)
![](https://user-gold-cdn.xitu.io/2019/5/25/16aed00cdadfef93?w=157&h=170&f=png&s=26843)
![](https://user-gold-cdn.xitu.io/2019/5/25/16aed00cfe9c253f?w=149&h=154&f=png&s=23722)
