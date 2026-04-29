<img width="1297" height="747" alt="image" src="https://github.com/user-attachments/assets/8bbe8f3b-9e8f-4585-95db-7ddbb2aff70c" /># OPLUS-Fastboot-Mode
为你的Oppo，或者丢失fastboot模式的OnePlus开启bootloader模式，也就是所谓的Fastboot模式，目前不解锁bootloader的情况下最高支持到天玑9000的Oppo-MTKV6的设备，只不过再往上却不行了。有可能在天玑9200更改了新的安全策略，刷入修改好的文件，设备无限启动
当然，俄罗斯已经有大佬将此原理和修改文件的工具发布了，所以我这发布的就是我之前做好的文件，正确刷入到对应设备对应的分区即可正常使用Fastboot

**1.准备工作**
需要准备好mtk工具，这里我很推荐刷机匣，他支持骁龙和MTK功能，功能实用广泛 
我们应该提前准备和adb工具包，里面应该有adb和fastboot的文件和dll才对，不然你输完指令会提示 **fastboot 不是内部或外部命令，也不是可运行的程序或批处理文件。**如果你找不到文件或者在哪下载，那我已经将文件放到了仓库中，下载解压之后，然后在目录路径最后方点一下，然后输入cmd再回车即可，
<img width="955" height="137" alt="1bde4796-d4a2-46f2-9544-4172ec89b446" src="https://github.com/user-attachments/assets/8153c9e2-abe4-4837-aaaf-f35ecad6ba1f" />

首次使用需要安装Linusb驱动和 刷机驱动 安装完成开始下一步
<img width="1393" height="859" alt="db6fda8b-b579-4f86-8b98-88d8a24de02a" src="https://github.com/user-attachments/assets/f33effc9-64e1-4511-8cbe-7ad761c335a1" />
**2.找到MTK功能，开始回读与刷写**
先选择配置，一般来说OPLUS天玑1200系列的可以不用选择，都是默认的da，如果你是高版本未熔断da的版本，端口是preloader的，需要选择对应芯片组的da，关于这些da我在另一个仓库放了https://github.com/xcacu06/MediaTek-DA
<img width="1393" height="859" alt="caec4fce-c726-4e84-8409-f09d2e7344c9" src="https://github.com/user-attachments/assets/a30a3dcb-4ca2-44b6-ba81-0bf109d20637" />
<img width="1185" height="838" alt="3c8a5a54-58d2-4e01-8e4b-921e8d0ad66c" src="https://github.com/user-attachments/assets/81e7b2ad-9717-48ae-8aef-5ef597052e07" />
点读取设备分区表，然后工具会进入等待模式
<img width="1393" height="859" alt="0da1e0e1-ad8d-4b7e-9b32-22807d8d4cef" src="https://github.com/user-attachments/assets/687b2c7e-44b5-4fa9-8f09-6cdb14feda67" />
<img width="1393" height="859" alt="ddb3b9c4-d342-4677-9fa6-3912fb59afe3" src="https://github.com/user-attachments/assets/f5a19980-7ad0-430b-a692-fc15cd21b3e7" />
此时你就可以连接手机了，进入mtk端口的方式有2种，可以在开启了adb状态的情况下，打开adb-cmd，输入adb reboot edl即可进入端口。
或者通过物理按键进入端口模式，通常是关机之后，同时按住音量加减然后插线，如果自动开机了，那么你可以按音量加减和电源键一起按住，直到工具识别，设备管理器出现端口即可松开。
连接成功了之后，分区表会有一个BOOT1,它就是我们要修改的东西了，如果你后期要更新系统的话，建议备份和在开始后面的操作
<img width="1393" height="859" alt="443a1b37-c89a-4b57-ac45-2a60d7f8e450" src="https://github.com/user-attachments/assets/703eed85-bd6e-48c6-b83d-a7df1a200a87" />
备份之后，就开始刷入我们的解锁文件了，选择所下载解锁文件的目录（提前解压好），然后选中它，完成之后开始刷入
<img width="926" height="379" alt="0e62b07f-2109-49bc-9fc8-d3d0251d004f" src="https://github.com/user-attachments/assets/3aa210b0-68bf-4e27-b516-d95a79ee240c" />
<img width="1393" height="859" alt="7148c1a0-4d47-4f57-9fa2-c4523438520d" src="https://github.com/user-attachments/assets/dae93170-5788-43a8-8750-7a8bc83d98fd" />
刷入完成之后，由于刷机匣对V5芯片组的重启有点问题，可能不能正常启动，所以可以直接拔线再插，手机的端口机制（通常是发送完da之后才会触发）就会自动重启设备，然后设备正常开机，像什么都没发生过，然后输入先去**开发者选项中提前开启OEM解锁**，然后输入adb指令
**adb reboot bootloader**来进入Fastboot 模式
进入Fastboot之后，通常有3行英文,部分出厂版本系统会有5行英文
<img width="1264" height="2077" alt="Screenshot_2026-04-30-00-18-09-51_99c04817c0de565" src="https://github.com/user-attachments/assets/9d62d5ab-bfcd-4739-9ba9-1affde1a4527" />
这个就是Fastboot模式了
然后我们执行解锁指令，
**fastboot flashing unlock**
设备会出现一大堆英文，我们只需要按一下音量加即可成功解锁。
然后我们输入fastboot reboot 即可重启手机
到此 你的设备已经解锁完成。
当然，你要保留Fastboot模式的情况，那么我建议你关闭系统自动更新和自动下载，如果你有更新系统的意向，那你就要用之前的刷写方式来还原你备份的文件。

对与MTK V6设备 原理也是如此，只不过首次刷入解锁文件之后要求格式化数据才能启动，然后后面步骤都差不多
**请一定看好处理器代号下载对应的解锁文件，混用将导致设备变砖！！！**
