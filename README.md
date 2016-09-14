# Base
Base是针对于Android开发封装好一些常用的基类，主要包括通用的Adapter、Activity、Fragment、Dialog等、和一些常用的Util类，为解耦而生。

##引入

###Maven：
```maven
<dependency>
  <groupId>com.king.base</groupId>
  <artifactId>Base</artifactId>
  <version>0.1</version>
  <type>pom</type>
</dependency>
```
###Gradle:
```gradle
compile 'com.king.base:Base:0.1'
```
###Lvy:
```lvy
<dependency org='com.king.base' name='Base' rev='0.1'>
  <artifact name='$AID' ext='pom'></artifact>
</dependency>
```
##依赖：
如果你项目中使用了RecyclerView控件请添加
```gradle
compile 'com.android.support:recyclerview-v7:24.0.0'//recyclerview随便哪个版本都可以，没有强制说使用24.0.0
```

```gradle
compile 'org.greenrobot:eventbus:3.0.0'
```

##简要说明：
Base主要实用地方体现在：出统一的代码风格，实用的各种基类，BaseActivity和BaseFragment里面还有许多实用的代码封装，只要用了Base，使用Fragment就感觉跟使用Activtiy基本是一样的。

##代码示例：

###通用的Adapter
```Java
/**
  * 
  * 只需继承通用的适配器（ViewHolderAdapter或ViewHolderRecyclerAdapter），简单的几句代码，妈妈再也不同担心我写自定义适配器了。
  */
public class TestAdapter extends ViewHolderAdapter<String> {


    public TestAdapter(Context context, List<String> listData) {
        super(context, listData);
    }

    @Override
    public View buildConvertView(LayoutInflater layoutInflater, String s, int position) {
        return inflate(R.layout.list_item);
    }

    @Override
    public void bindViewDatas(ViewHolder holder, String s, int position) {
        holder.setText(R.id.tv,s);
    }
}

```

###基类BaseActivity
```Java
public class TestActivity extends BaseActivity {

    private TextView tv;
    private Button btn;

    @Override
    public void initUI() {
        //TODO:初始化UI
        setContentView(R.layout.activity_test);
        tv = findView(R.id.tv);
        btn = findView(R.id.btn);
    }

    @Override
    public void addListeners() {
        //TODO:添加监听事件
    }

    @Override
    public void initData() {
        //TODO:初始化数据（绑定数据）
        tv.setText("text");
    }

    @Override
    public void onEventMessage(EventMessage em) {
        //TODO:接收EventBus发送的事件（EventMessage）
    }
}
```

###BaseFragment
```Java
public class TestFragment extends BaseFragment {
    @Override
    public int inflaterRootView() {
        return R.layout.fragment_test;
    }

    @Override
    public void initUI() {
        //TODO:初始化UI
    }

    @Override
    public void addListeners() {
        //TODO:添加监听事件
    }

    @Override
    public void initData() {
         //TODO:初始化数据（绑定数据）
    }

    @Override
    public void onEventMessage(EventMessage em) {
        //TODO:接收EventBus发送的事件（EventMessage）
    }
}
```
###BaseDialogFragment
```Java
public class TestDialogFragment extends BaseDialogFragment {
    @Override
    public int inflaterRootView() {
        return R.layout.fragment_test_dialog;
    }

    @Override
    public void initUI() {
        //TODO:初始化UI
    }

    @Override
    public void addListeners() {
        //TODO:添加监听事件
    }

    @Override
    public void initData() {
        //TODO:初始化数据（绑定数据）
    }

    @Override
    public void onEventMessage(EventMessage em) {
         //TODO:接收EventBus发送的事件（EventMessage）
    }
}
```
###其他小功能

使用Log:
统一控制管理Log
```Java
 LogUtils.v(); 
 
 LogUtils.d();
 
 LogUtils.i();
 
 LogUtils.w();
 
 LogUtils.e();
 
 LogUtils.twf();
 
 LogUtils.println();
```

直接使用[EventBus](https://github.com/greenrobot/EventBus)：
    不管是BaseActivity还是BaseFragment的基类中都可以直接使用EventBus的功能。
    在BaseActivity有如下方法
```Java
    public static void sendEvent(Object obj){
        EventBus.getDefault().post(obj);
    }
```
发送事件用法
```Java
 sendEvent（new EventMessage（1））; //这个可以直接在onEventMessage方法中取接收发送的事件消息
```
```Java
 sendEvent(obj);//或者直接这个需要自己取接收，使用的方法请参照EventBus
```

使用Toast
```Java
 showToast(CharSequence text);
 
 showToast(@StringRes  int resId);
```

使用Dialog
```Java
 showDialog(View v);
```
```Java
 showProgressDialog();
 
 showProgressDialog(@LayoutRes int resId);
 
 showProgressDialog(View v);
```

更多实用黑科技，请速速使用Base体会吧。


## License

    Copyright © 2015, 2016 Jenly Yu 

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

