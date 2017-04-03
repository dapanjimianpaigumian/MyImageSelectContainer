# MyImageSelectContainer
高仿微信_朋友圈图片上传与头像上传_正常版
本项目实现了类似微信那种选择头像和上传图片的功能

1. 功能介绍：

  可根据传入的值控制是选择头像还是上传图片，大于1就是选择图片，等于1救是选择头像
  
  可根据传入的值控制选择图片的数量，并且当选中的图片数量等于这个数量时，则其他没有被选中的图片变成不可选择
  
  可选择不同文件夹下的图片
  
  自定义ViewGroup显示选中的图片数，不同的数量显示的格式不一样（gif最后那一帧录制的不是很清楚），类似微信那种，1张，2张还是9张显示的格式不同
  
  拍照剪切头像
  
2. 实现思路：

  在子线程中读出sd卡下所有的文件夹下的图片，并且在RecyclerView中显示出来
  
  RecyclerView采用多item布局方式，分开拍照和图片，主要是方便修改拍照的view，这里只是用图片显示

  适配每个图片等宽度和高度为屏幕宽度等三分之一

  底部采用PopupWindow显示出所有的图片所在的文件夹

  如果是多选图片，则为每个view添加checkbox的选中监听，否则就调用系统的剪切图片功能，剪切完成之后显示出来

  根据选中的图片数，展示不同的布局
  
3.需要注意的地方：

  如何处理选中图片，图片数量达到最大可选数和取消选中图片的时候，RecyclerView刷新时数据不会错乱
  
  如何处理RecyclerView复用时，数据不会错乱
  
  其实实现的思路时一样，给bean对象添加一个子段，记录当前图片等状态，根据状态来改变view等状态，相信有些人会遇到checkbox复用等时候到坑，
  当RecyclerView复用的时候，checkbox的OnChangeListener是一定会触发，它有两个状态，选中和没选中，所以，我们需要在复用等时候去做处理，
  个人认为最好的办法就是在bean中记录状态，不仅能保证数据的正确性，也是最容易处理，万物皆对象嘛。
  http://www.jianshu.com/p/c82d4ab45c20
