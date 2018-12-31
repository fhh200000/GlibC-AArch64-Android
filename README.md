Compiled GlibC libraries for Android mobiles with AArch64 instruction sets.  
为具有AArch64指令集的安卓设备编译的GlibC运行库。  
Note that due to the Bionic runtime libraries,you should spicify the linker to ld-linux-aarch64.so.1 in lib folder.  
注意，因为自带的Bionic运行库造成的干扰，您需要将链接器指定为lib文件夹下的ld-linux-aarch64.so.1。  
A big advantage is that you can run NATIVE AArch64 Linux softwares with only few changes.  
一个优势：现在您只需极其少量的操作就可以使为Linux AArch64架构编译的应用程序成功运行。  
A utility called 'patchelf',linked with native Android linker,is attached to the GlibC.  
(Source from NixOS:https://nixos.org/patchelf.html)  
一个使用了原生安卓链接器、名为"patchelf"的工具，已经附在了GlibC工具包里。  
You can patch the Native Linux executable files by using the following command(Dynamic libraries are not needed to be patched):  
您可以使用以下的命令为原生Linux程序制作补丁(动态链接库不需要修补)：  
<pre><code>patchelf --set-rpath (/path/to/glibc)/lib:(/path/to/glibc)/lib64 YourProgram
patchelf --set-interpreter (/path/to/glibc)/lib/ld-linux-aarch64.so.1 YourProgram</code></pre>  
<label style="color: red">NOTE:PLEASE DO NOT SET "LD_LIBRARY_PATH" INSTEAD.IT WILL LET ANDROID LINKER CONFUSED.</label>  
<label style="color:red">注意：不要设置“LD_LIBRARY_PATH”变量来代替修补。这样会造成安卓的链接器错误链接。</label>  
You can also compile programs yourself since there are full headers attached.  
您也可以使用这份GlibC自行编译程序，因为这里有完整的头文件附带。  
Using your cross-compile chain(tested GCC) with '-L(/path/to/glibc/on/PC) -Wl,-R(/path/to/glibc/on/Android) -Wl,-dynamic-linker=(/path/to/glibc)/lib/ld-linux-aarch64.so.1' command to build.  
使用您的交叉编译链（已测试GCC），并添加"-L(/path/to/glibc/on/PC) -Wl,-R(/path/to/glibc/on/Android) -Wl,-dynamic-linker=(/path/to/glibc)/lib/ld-linux-aarch64.so.1"的参数来构建。  
If you want to build C++ programs or multi-threaded programs,please compile libstdc++ and libgcc by instructions provided by GCC.  
如果您希望构建C++程序或者多线程程序的话，请遵循GCC的指导构建libstdc++和libgcc。  
