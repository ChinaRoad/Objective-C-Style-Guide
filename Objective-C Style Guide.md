#深圳市神州路路通网络科技有限公司Objective-C编码规范

### 文档版本更新历史
##### 2013-11-13 1.0.3

	更新1-10-2，修改错别字。
	更新1-10-2，增加了代码块超过5行后和前面的花括号之间必须空一行的约定。
	增加1-10-3，else和前面的右花括弧之间必须空一行的约定。
	增加1-11，常量定义相关约定。
	更新4-16，更新示例代码的风格

##### 2013-08-12 1.0.2
    增加1-10，对代码中左花括号的位置的说明。并相应的更新了本文档中的相关实例代码。

##### 2013-07-22 1.0.1
    
    增加3-1，注释采用Javadoc风格规范

##### 2013-07-22 1.0.0

###参考资料

* Apple: [Coding Guidelines for Cocoa](http://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html)
* Google: [Objective-C Style Guide](http://google-styleguide.googlecode.com/svn/trunk/objcguide.xml)
* CocoaChina: [Daniel's Objective-C Coding Style Guidelines](http://www.cocoachina.com/bbs/read.php?tid=36545&keyword=%B1%E0%C2%EB%B9%E6%B7%B6)




##1. 代码的格式化

#### 1-1. 指针符号 "*" 靠近变量名字
    
    NSString* varName; //错误
    NSString *varName; //正确
    
#### 1-2. 只用空格缩进，1个TAB = 4个空格字符

    在XCode->Preferences->Text Editing->Indentation中进行如下设置：
    1. Prefer indent using: 选择 Spaces
    2. Tab key：选择 Intents in leading whitespace
    3. 所有需要填写空格数目的地方都设置成4个
    
#### 1-3. 代码每行长度最多不超过100个字符

    为了防止代码过长，也为了兼顾Macbook上的排版效果，将每行长度限制成100个字符
    
    Google倡导的每行80个字符有点少，会带来更频繁的换行，因此增加到100个字符。
    
    勾选XCode->Preferences->Text Editing->Editing，并将长度设置成100来打开行宽指示。
    
#### 1-4. 尽量将单个方法的实现代码控制在30行内

    如果单个方法的实现代码过长，要考量将代码拆分成几个小的方法。
    
#### 1-5. 尽量将单个实现文件的代码行数控制在500～600行内

    单个实现文件的代码行数保持在500～600行以内最好。当接近或超过800行时，就应当考量要分割实现文件了。
    
    可以使用Objective-C的Category特性将实现文件归类分割成几个相对轻量级的实现文件。
    可以勾选上XCode->Preferences->Text Editing->Editing中的Line numbers，开启行号提示。
    
#### 1-6. 方法的声明和定义

##### 1-6-1. 在 - 或 + 和返回值之间留1个空格，方法名和参数列表间不留空格

    - (void)invokeWithTarget:(id)target; //正确
    - (void)invokeWithTarget: (id)target; //错误
    - (void)invokeWithTarget:(id) target; //错误
    - (void)invokeWithTarget: (id) target; //错误
    
##### 1-6-2. 参数过多超过一行时，每个参数占用一行，以冒号对齐

    - (void)doSomethingWith:(GTMFoo *)theFoo
                       rect:(NSRect)theRect                   interval:(float)theInterval;
##### 1-6-3. 方法名第一段关键字比其他部分短时，每个参数占用一行，每行至少缩进4个空格，尽量保持参数以冒号对齐
    - (void)short:(GTMFoo *)theFoo
              longKeyword:(NSRect)theRect
        evenLongerKeyword:(float)theInterval
                    error:(NSError **)theError; 
                    
#### 1-7. 方法的调用

##### 1-7-1. 调用方法沿用方法声明和定义的习惯。如果给定源文件已经遵从某种习惯，继续遵从那种习惯

##### 1-7-2. 如果方法调用中包含内嵌的block代码，block代码整体应该至少缩进4个空格符（详情参见后面的Blocks部分）

#### 1-8. 协议声明或定义中，类型标识符、协议名称、尖括号之间不留空格

    @interface MyProtocoledClass : NSObject<NSWindowDelegate> 
    {
        @private
        id<MyFancyDelegate> _delegate;
    }
    
    - (void)setDelegate:(id<MyFancyDelegate>)aDelegate;
    @end
    
#### 1-9. Blocks

##### 1-9-1. Block里面的代码应该整体缩进4个空格

##### 1-9-2. 如果Block里面的代码一行可以写得下，就不需要换行

    如：
    [operation setCompletionBlock:^{ [self onOperationDone]; }];
    
##### 1-9-3. 如果需要换行时，结尾的花括弧要和声明block那一行的第一个字符对齐

    如：
    [operation setCompletionBlock:^{
        [self.delegate newDataAvailable];
    }];
    
##### 1-9-4. 如果调用部分的代码过长，造成内嵌的block代码缩进过长，可以适当的增加手动换行，以减少代码缩进。

    如以下代码在loadWindowWithCompletionBlock前加了手动换行，是允许的：
    [[SessionService sharedService]
        loadWindowWithCompletionBlock:^(SessionWindow *window) {
            if (window) {
            
                [self windowDidLoad:window];
            } else {
                
                [self errorLoadingWindow];
            }
    }];
    
    
    
##### 1-9-5. 如果Block没有参数，^{之间没有空格。如果block有参数，^(之间没有空格，) {之间有一个空格。 

#### 1-10. 花括号的位置

##### 1-10-1. 实现文件中，函数体的左花括号另起一行，不和函数名同行。
    如下：
    //错误
    - (void)didReceiveMemoryWarning {
    
        [super didReceiveMemoryWarning];
        // Dispose of any resources that can be recreated.
    }
    
    //正确
    - (void)didReceiveMemoryWarning 
    {
        [super didReceiveMemoryWarning];
        // Dispose of any resources that can be recreated.
    }
    
##### 1-10-2. 方法或函数体中，流程控制(if, while, switch等)相关代码中的左花括号不单独一行。但是左花括号后面紧接着的代码块超过5行后，代码块和括号之间要有一行空行；代码块小于5行可以不空行。
    如：
    //错误
    - (void)didReceiveMemoryWarning 
    {
        [super didReceiveMemoryWarning];
        // Dispose of any resources that can be recreated.
        
        if (somethCondtion) 
        {
            //DO Something
        }
    }
    
    //正确
    - (void)didReceiveMemoryWarning 
    {
        [super didReceiveMemoryWarning];
        // Dispose of any resources that can be recreated.
        
        if (somethCondtion) {
        
            //DO Something. 
        }
    }
    
    此条是为了兼容XCode代码提示生成的代码。
    
##### 1-10-3. if-else中，}和else之间需要换行

	如：
	//错误
	if (a > 0) {
	
		//Do Something
	} else {
	
		//Do Something
	}
	
	//正确
	if (a > 0) {
	
		//Do Something
	} 
	else {
	
		//Do Something
	}
	
	此条是为了防止else和上一个if代码块挨在一起，影响阅读。

#### 1-11. 常量定义

##### 1-11-1. 创建NSString, NSDictionary, NSArray, 以及NSNumber等常量时，使用Literals语法。

	//例如：
	NSArray names = @[@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul"];
	NSDictionary productManagers = @{@"iPhone" : @"Kate", @"iPad" : @"Kamal", @"Mobile Web" : @"Bill"}; 
	NSNumber shouldUseLiterals = @YES; 
	NSNumber buildingZIPCode = @10018; 
	
	//而不是：
	NSArray names = [NSArray arrayWithObjects:@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul", nil]; 
	NSDictionary productManagers = [NSDictionary dictionaryWithObjectsAndKeys: @"Kate", @"iPhone", @"Kamal", @"iPad", @"Bill", @"Mobile Web", nil]; 
	NSNumber shouldUseLiterals = [NSNumber numberWithBool:YES]; 
	NSNumber ZIPCode = [NSNumber numberWithInteger:10018];
	
##### 1-11-2. 定义枚举时，使用NS_ENUM或NS_OPTIONS。因为NS_ENUM和NS_OPTIONS都提供了类型检查。

	//例如：
	typedef NS_ENUM(NSUInteger, PPNavBarButtonColor) {
	    PPNavBarButtonColorBlack,
	    PPNavBarButtonColorGreen,
	    PPNavBarButtonColorDefault = PPNavBarButtonColorBlack
    };
    
    typedef NS_OPTIONS(NSUInteger, PSTCollectionViewScrollPosition) {
	    PSTCollectionViewScrollPositionNone                 = 0,
	
	    PSTCollectionViewScrollPositionTop                  = 1 << 0,
	    PSTCollectionViewScrollPositionCenteredVertically   = 1 << 1,
	    PSTCollectionViewScrollPositionBottom               = 1 << 2,
	
	    PSTCollectionViewScrollPositionLeft                 = 1 << 3,
	    PSTCollectionViewScrollPositionCenteredHorizontally = 1 << 4,
	    PSTCollectionViewScrollPositionRight                = 1 << 5
    };



## 2. 命名规范

#### 2-1. 文件名应该要能反映出它包含的类的名称
    
    如：NSString.h 和 NSString.m 包含了NSString类的定义和实现。
    
#### 2-2. Category的文件名要包含它所扩展的那个类的名称

    如：UIImage+Resize.h 或 UIImage+TintColor.h
    
#### 2-3. 类名、类别名字及协议名字，都采用大驼峰式命名规则。即每个单词的首字母都大写。

    如：DataManager
    
#### 2-4. 在面向特定应用的代码中，类名尽量避免使用前缀，每个类都使用相同的前缀会影响可读性。

#### 2-5. 在面向多应用的代码中，类名推荐使用前缀。

    如：UIImage、GTMSendMessage
    
#### 2-6. 类别名字

    待定

#### 2-7. 方法名

##### 2-7-1. 方法名的首字母小写，且使用首字母大写的形式分割单词。参数使用相同的规则。

##### 2-7-2. 方法名+参数名应该尽量读起来像一句话。具体参见[苹果的方法名命名规范](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CodingGuidelines/Articles/NamingMethods.html)

    如：convertPoint:fromRect: 或者 replaceCharactersInRange:withString:
    
##### 2-7-3. 当各个参数是接收者的某个属性时，方法名中不要用"and"来连接

    //正确
    - (int)runModalForDirectory:(NSString *)path file:(NSString *) name types:(NSArray *)fileTypes;
    //错误
    - (int)runModalForDirectory:(NSString *)path andFile:(NSString *)name andTypes:(NSArray *)fileTypes;
    
##### 2-7-4. 如果方法名描述了两种不同的动作，要使用"and"来连接

    - (BOOL)openFile:(NSString *)fullPath withApplication:(NSString *)appName andDeactivate:(BOOL)flag;
    
##### 2-7-5. getter方法的方法名应该和变量名字相同，不允许使用"get"前缀。

    //本规则仅仅适用于Objective-C，C++使用C++的相关规范
    - (id)getDelegate;    //禁止
    - (id)delegate;    // 正确

##### 2-7-6. 类私有方法以下划线开头。
    
    如：- (void)_startDownloadFiles;
    
    备注：Objective-C里面没有真正严格意义上私有方法。这里所说的"私有方法"指那些不需要公开的、只会在实现文件中使用的方法。
    
    这样做的好处是，可以直观的快速区别实现文件中的私有方法和公有方法。
    
    另外，如果某个方法废弃了，需要移除的时候，发现它是以下划线开头的，那么就可以确定这个方法是私有的，只会在这个实现文件中被用到。那么直接在该实现文件搜索这个方法的名字，然后清理掉搜索到的地方就可以了。不必再在整个项目中查找是否没有清理干净。
    
    此条不做强制。按苹果的说法，可能覆盖掉官方的私有方法。但是通过我一年多的使用经验看，还没有遇到过覆盖掉官方私有方法的情况。
    
#### 2-8. 函数名

##### 2-8-1. 函数名命名规则基本和方法名命名规则一致，但有以下例外：

##### 2-8-2. 如果函数和某个特定类相关，那么函数前缀要和类的前缀一样。

##### 2-8-3. 第一个单词的首字母要大写

    
    
#### 2-9. 属性名和变量名

##### 2-9-1. 变量名字采用小驼峰式命名规则。即第一个单词的首字母小写，且使用首字母大写的方式分割单词

##### 2-9-2. 实例变量以下划线开头

    如：_myInstanceVariable
    
##### 2-9-3. 禁止使用匈牙利标记法来标记变量，变量名应该尽量清楚的描述它的用途。这样可以使别人立即明白代码的意思，所以不要担心这样会导致代码过长。

    //以下这些都是错误的命名规范
    int w;
    int nerr;
    int nCompConns;
    tix = [[NSMutableArray alloc] init];
    obj = [someObject object];
    p = [network port];
    
    //以下这些才是正确的命名规范
    int numErrors;
    int numCompletedConnections;
    tickets = [[NSMutableArray alloc] init];
    userInfo = [someObject object];
    port = [network port];
    
##### 2-9-4. 常量（#defines，枚举，局部常量）名字以小写k字母开头，以首字母大写的方式来分割单词。

    如：
    #define kOperationDoneNotification @"kOperationDoneNotification"
    const int kNumberOfFiles = 12;
    NSString *const kUserKey = @"kUserKey";
    enum DisplayTinge {
        kDisplayTingeGreen = 1,
        kDisplayTingeBlue = 2
    };
    
##### 2-9-5. 和特定类相关的枚举常量使用类名作为前缀，而不必用小写k开头。

    如：
    typedef enum {
        UITableViewStylePlain,
        UITableViewStyleGrouped
    } UITableViewStyle;
    
##### 2-9-6. #define和const，优先使用const定义常量。

##### 2-9-7. 如果一个常量只在某一个特定的文件中使用，用static关键字修饰它

    static关键字保证变量只有文件作用域，可以避免变量名重名造成的链接错误问题。
    
#### 2-10. 通知名字和异常名字

##### 2-10-1. 通知名字的命名规则
    
    [相关联的类名字] + [Did | Will] + [独一无二的一段名称] + Notification
    
    如：UIApplicationDidBecomeActiveNotification
    
##### 2-10-2. 异常名字的命名规则

    [前缀] + [独一无二的一段名称] + Exception
    
    如：NSColorListIOException
    
## 3. 注释

#### 3-1. 注释采用[Javadoc](http://en.wikipedia.org/wiki/Javadoc)风格规范

    因为XCode5支持直接将Javadoc风格的注释导出生成文档。
    另外XCode也有用于添加Javadoc风格注释的插件：VVDocumenter-Xcode(https://github.com/onevcat/VVDocumenter-Xcode)

## 4. Cocoa和Objective-C特有规则

#### 4-1. 实例变量

##### 4-1-1. 要避免声明@public属性的实例变量

##### 4-1-2. 实例变量应该被声明成@private或@protected属性

##### 4-1-3. 如果你希望别人在重载你的类的时候能够直接访问内部数据，可以将实例变量声明成@protected的

#### 4-2. 注释并且清楚的指出哪一个初始化方法是你的指定初始化方法（Designated Initializer）

    明确的指出哪一个初始化方法是你的类的指定初始化方法，这样当别人想重载你的类的时候，就可以避免重载多个初始化方法，只需要重载这个指定的初始化方法就可以了。也能够帮助别人在需要时能够很容易明白你的类的初始化流程。
    
#### 4-3. 重载指定初始化方法

    待定

#### 4-4. 重载时，将NSObject相关的一些需要重载的方法放到@implementation的顶部

    比如init..., copyWithZone:, 以及dealloc这些方法，重载时都推荐放在@implementation的顶部。
    特别时dealloc方法，应该放在@implementation顶部的第一个，这样会时刻提醒你要记得释放相关资源。
    
#### 4-5. 在初始化方法中，不要将实例变量初始化为0或nil。这是多余的

    所有新创建的对象的内存都会被初始化为0（isa除外），所以不需要重复初始化为0或nil。

#### 4-6. 要避免时用 +new 方法

    不要调用NSObject的类方法+new，也不要在子类中重载它。使用alloc和init方法代替。现代的Objective-C已经明确的使用alloc和init方法来创建一个对象。new方法已经很少用了，review代码时，它会将检查内存泄漏的工作变得更困难。所以避免使用它。 
    
#### 4-7. 保持公有API的简洁性

    如果一个API没有必要公开，就把它归类到私有类别里面去，而不公开在头文件中。
    
#### 4-8. 使用#import引入Objective-C和Objective-C++头文件，使用#include引入C和C++头文件

待完善

#### 4-9. import根框架，而非单个文件 

    虽然有时我们仅需要框架中的某几个头文件，但引入根文件编译器会运行的更快。因为根框架一般都会被预编译，所以加载会更快。
    
#### 4-10. Dealloc的顺序要与变量声明的顺序相同。如果dealloc中调用其他方法来release变量，要注释清楚这个方法release了哪些变量。

    这样有利于review代码。
    
#### 4-11. NSString类型的property优先选择copy。尽量避免对NSString使用retain

    如：
    - (void)setFoo:(NSString *)aFoo 
    {
        [_foo autorelease];
        _foo = [aFoo copy];
    }
    
    这是为了避免外部调用者在你不知道或不期望的情况下改变它的值。不要认为它一定是一个NSString的参数，有可能调用者实际传递给你的是一个NSMutableString。
    
#### 4-12. 避免抛出异常

    待定
    
#### 4-13. 仅在有业务逻辑需求时检查nil，而非为了防止崩溃

    向nil发送消息不会导致系统崩溃，Objective-C运行时会负责处理。
    注意：由于Objective-C运行时不会处理给NULL指针的情况，所以为了避免崩溃，你需要自行处理对于C/C++的NULL指针的检测。
    
#### 4-14. Objective-C中，只允许使用BOOL。禁止将int直接转换为BOOL。将整形转换成BOOL时，应当使用三元运算符返回YES或NO，或者使用位运算符(&&, || , !)。

    将int转换成BOOL时要特别小心。避免直接使用int和YES做比较。
    因为在Objective-C中，BOOL被定义为signed char。这意味着除了YES(1)和NO(0)之外，它还可以是其他值。
    
    //以下都是被禁止的
    - (BOOL)isBold 
    {
        return [self fontTraits] & NSFontBoldTrait;
    }
    - (BOOL)isValid 
    {
        return [self stringValue];
    }
    
    //以下才是正确的方式
    - (BOOL)isBold 
    {
        return ([self fontTraits] & NSFontBoldTrait) ? YES : NO;
    }
    - (BOOL)isValid 
    {
        return [self stringValue] != nil;
    }
    - (BOOL)isEnabled 
    {
        return [self isValid] && [self isBold];
    }
    
#### 4-15. 禁止将BOOL直接和YES比较

    如：
    //以下是禁止的
    BOOL great = [foo isGreat];
    if (great == YES)
        // ...be great!
        
    //以下是正确的
    BOOL great = [foo isGreat];
    if (great)
        // ...be great!
        
#### 4-16. 多层嵌套的if语句，编码时优先考虑条件不成立可以立即跳出的情况

    比如：
    if (a) {
    
        if (b) {
        
            //do something
        } 
        else {
        
            return;
        }
    } 
    else {
    
        return;
    }
    
    改成优先考量可以跳出的情况，这样可以有效的减少代码缩进长度：
    if (!a) {
    	return;
    }
        
    if (!b) {
	    return;
    }
        
    //do something
    

    
    
    
  
    





