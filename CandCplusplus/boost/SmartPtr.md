# boost库智能指针

智能指针是存储指向动态分配（堆）对象的指针的对象。 它们的行为与内置的C++指针非常相似，只是它们会自动删除在适当的时间指向的对象。 智能指针在面对异常时特别有用，因为它们可确保正确销毁动态分配的对象。 它们还可用于跟踪多个所有者共享的动态分配对象。

从概念上讲，智能指针被视为拥有指向的对象，因此在不再需要时负责删除对象。 因此，它们是Bjarne Stroustrup的“The C ++ Programming Language”，第3版，第14.4节，资源管理中描述的“资源获取是初始化”的例子。

该库提供了六个智能指针类模板：

* scoped_ptr，用于包含当前作用域的动态分配对象的所有权;

* scoped_array，为动态分配的数组提供范围所有权;

* shared_ptr，一种用于管理对象或数组的共享所有权的通用工具;

* weak_ptr，一个shared_ptr管理对象的非拥有观察者，可以暂时提升为shared_ptr;

* intrusive_ptr，指向具有嵌入引用计数的对象的指针;

* local_shared_ptr，在单个线程中提供共享所有权。

自2011年迭代以来，shared_ptr和weak_ptr是C++标准的一部分。此外，该库包含以下支持实用程序功能和类：

* make_shared，一个用于创建返回shared_ptr的对象的工厂函数;

* make_unique，一个返回std :: unique_ptr的工厂函数;

* enable_shared_from_this，一个辅助基类，可以获取指向此的shared_ptr;

* pointer_to_other，用于将一个智能指针类型转换为另一个智能指针类型的辅助特征;

* static_pointer_cast和companions，通用智能指针转换;

* intrusive_ref_counter，一个包含引用计数的辅助基类。

* atomic_shared_ptr，一个帮助类，它实现std :: atomic的接口，类型为shared_ptr。

作为一般规则，不允许对库中指针管理的对象的析构函数或运算符删除抛出异常。
