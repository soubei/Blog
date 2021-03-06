### 1.创建数据表迁移文件

```
php artisan make:migration create_user_table
```
### 2.在创建的迁移文件中设置表属性，字段等。

```
public function up()
    {
        Schema::create('blog_article',function(Blueprint $table){
            $table->increments('article_id')->index();
            $table->integer('author_id')->index();
            $table->integer('article_pid');
            $table->timestamp('created_at');
            $table->string('article_title');
            $table->text('content');
        });
    }
```
### 3.创建数据表

```
php artisan migrate
```
### 4.创建控制器

```
php artisan make:controller UserController
```
这条命令会在app/Http/Controller下创建UserController.php文件
如果在别的命名空间下创建控制文件，可在命令中带命名空间

```
php artisan make:controller Admin\UserController
```
### 5.创建RESTful资源型控制器

```
php artisan make:controller Admin\UserController --resource
```
这条命令会在Http/Admin下创建控制器UserController.php ，并且控制器中带有7个方法。

```
    public function index()
        {
            //

        }


        public function create()
        {
            //

        }


        public function store(Request $request)
        {


        }


        public function show($id)
        {
            //
        }


        public function edit($id)
        {

        }


        public function update(Request $request, $id)
        {


        }


        public function destroy($id)
        {

        }
```
使用命令可以查看这几个方法对应的路由以及作用

```
php artisan route:list
```
### 6.查看php artisan 命令

```
php artisan
```
列表显示laravel的各种命令。

```
    PS G:\www\blog> php artisan
    Laravel Framework version 5.2.45

    Usage:
      command [options] [arguments]

    Options:
      -h, --help            Display this help message
      -q, --quiet           Do not output any message
      -V, --version         Display this application version
          --ansi            Force ANSI output
          --no-ansi         Disable ANSI output
      -n, --no-interaction  Do not ask any interactive question
          --env[=ENV]       The environment the command should run under.
      -v|vv|vvv, --verbose  Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug

    Available commands:
      clear-compiled      Remove the compiled class file
      down                Put the application into maintenance mode
      env                 Display the current framework environment
      help                Displays help for a command
      list                Lists commands
      migrate             Run the database migrations
      optimize            Optimize the framework for better performance
      serve               Serve the application on the PHP development server
      tinker              Interact with your application
      up                  Bring the application out of maintenance mode
     app
      app:name            Set the application namespace
     auth
      auth:clear-resets   Flush expired password reset tokens
     cache
      cache:clear         Flush the application cache
      cache:table         Create a migration for the cache database table
     config
      config:cache        Create a cache file for faster configuration loading
      config:clear        Remove the configuration cache file
     db
      db:seed             Seed the database with records
     event
      event:generate      Generate the missing events and listeners based on registration
     key
      key:generate        Set the application key
     make
      make:auth           Scaffold basic login and registration views and routes
      make:console        Create a new Artisan command
      make:controller     Create a new controller class
      make:event          Create a new event class
      make:job            Create a new job class
      make:listener       Create a new event listener class
      make:middleware     Create a new middleware class
      make:migration      Create a new migration file
      make:model          Create a new Eloquent model class
      make:policy         Create a new policy class
      make:provider       Create a new service provider class
      make:request        Create a new form request class
      make:seeder         Create a new seeder class
      make:test           Create a new test class
     migrate
      migrate:install     Create the migration repository
      migrate:refresh     Reset and re-run all migrations
      migrate:reset       Rollback all database migrations
      migrate:rollback    Rollback the last database migration
      migrate:status      Show the status of each migration
     queue
      queue:failed        List all of the failed queue jobs
      queue:failed-table  Create a migration for the failed queue jobs database table
      queue:flush         Flush all of the failed queue jobs
      queue:forget        Delete a failed queue job
      queue:listen        Listen to a given queue
      queue:restart       Restart queue worker daemons after their current job
      queue:retry         Retry a failed queue job
      queue:table         Create a migration for the queue jobs database table
      queue:work          Process the next job on a queue
     route
      route:cache         Create a route cache file for faster route registration
      route:clear         Remove the route cache file
      route:list          List all registered routes
     schedule
      schedule:run        Run the scheduled commands
     session
      session:table       Create a migration for the session database table
     vendor
      vendor:publish      Publish any publishable assets from vendor packages
     view
      view:clear          Clear all compiled view files

```
### 7.创建模型

```
php artisan make:model User
```
这条命令会在app下创建一个模型文件User.php

```
php artisan make:model Http\Model\User
```
这条命令会在app/Http/Model下创建模型文件User.php
### 8.安装laravel

```
composer create_project larvel/laravel --prefer-dist
```
### 9.laravel/laravel和laravel/framework
laravel/laravel：laravel框架的示例程序，已经包含laravel框架源代码和其他的外部库
laravel/framework：仅仅Laravel框架的源代码
### 10.laravel 5.2php版本要求
- PHP >= 5.5.9
- OpenSSL PHP Extension
- PDO PHP Extension
- Mbstring PHP Extension
- Tokenizer PHP Extension

### 11. 生成每台电脑唯一的key

```
php artisan key generate
```
### 12.laravel路由有几种

```
    Route::get($uri, $callback);
    Route::post($uri, $callback);
    Route::put($uri, $callback);
    Route::patch($uri, $callback);
    Route::delete($uri, $callback);
    Route::options($uri, $callback);
```
### 13响应多个路由

```
    Route::match(['get', 'post'], '/', function () {
        //
    });

    Route::any('foo', function () {
        //
    });
```
### 14.路由传参（必传）


```
    Route::get('/shenhe/{art_id}','ArticleController@shenhe');
    //文章上架
    Route::get('/up/{art_id}','ArticleController@up');
    //文章下架
    Route::get('/stop/{art_id}','ArticleController@stop');
```
注意： 路由参数不能包含 - 字符。请用下划线 (_) 替换。
### 15.路由传参（可选）


```
    Route::get('user/{name?}', function ($name = null) {
        return $name;
    });

    Route::get('user/{name?}', function ($name = 'John') {
        return $name;
    });
```
### 16.路由命名

```
    Route::get('user/profile', [
    'as' => 'profile', 'uses' => 'UserController@showProfile'
]);
```
这个路由名称为profile

### 17.路由群组

```
    Route::group(['middleware'=>['web'],'namespace'=>'Home'],function(){
        Route::get('/', 'IndexController@index');
        Route::get('/article/{art_id}', 'ArticleController@index');
        Route::get('/cate/{cate_id}', 'ArticleController@cate');

    });
```

### 18.对命名路由生成urls

```
    $url = route('profile');

    $redirect = redirect()->route('profile');
```
### 19.路由前缀

```
    Route::group(['middleware'=>['web'],'prefix'=>'admin','namespace'=>'Admin'],function(){
    //后台登录
    Route::any('/login','LoginController@login');

    //验证码路由
    Route::get('/code','LoginController@code');
});
```
### 20.什么是CSRF保护

```
Laravel 会自动生成一个 CSRF token 给每个用户的 Session。该token用来验证用户是否为实际发出请求的用户。可以使用 csrf_field 辅助函数来生成一个包含 CSRF token 的
```
### 21.模板中使用csrf保护

```
    {{ csrf_field() }}
```
### 22.ajax在laravel框架中的使用(删除)

```
    /*文章-删除*/
        function article_del(obj,id){
            $.ajaxSetup({
                headers: {
                    'X-CSRF-TOKEN': $('input[name="_token"]').val()
                }
            });
            layer.confirm('确认要删除吗？',function(index){
                $.ajax({
                    type: 'delete',
                    url: "{{url('admin/article')}}"+"/"+id,
                    success: function(data){
                        if(data.status==1){
                            $(obj).parents("tr").remove();
                           layer.msg('已删除!',{icon:1,time:1000});
                        }else{
                            layer.msg('已删除!',{icon:5,time:1000});
                        }
                    }
                });
            });
        }
```
### 23.ajax在laravel框架中的使用(新增)

```
    $("#form-article-add").validate({

                onkeyup:false,
                focusCleanup:true,
                success:"valid",
                submitHandler:function(form){
                    $(form).ajaxSubmit({
                        url:"{{url('admin/article')}}",
                        type:'post',
                        success:function(data){

                            if(data.status==1){
                                layer.msg(data.msg,{icon:6},function(){
                                    var index = parent.layer.getFrameIndex(window.name);
                                    parent.window.location.reload();
                                    parent.layer.close(index);
                                });
                            }else if(data.status==0){
                                layer.msg(data.msg,{icon:5});
                            }
                        }
                    });
                }
            });
```

### 24.ajax在laravel框架中的使用（编辑）

```
$("#form-article-edit").validate({

                onkeyup:false,
                focusCleanup:true,
                success:"valid",
                submitHandler:function(form){
                    $(form).ajaxSubmit({
                        url:"{{url('admin/article/'.$data->art_id)}}",
                        type:'put',
                        success:function(data){
                            if(data.status==1){
                                layer.msg(data.msg,{icon:6},function(){
                                    var index = parent.layer.getFrameIndex(window.name);
                                    parent.window.location.reload();
                                    parent.layer.close(index);
                                });
                            }else if(data.status==0){
                                layer.msg(data.msg,{icon:5});
                            }
                        }
                    });
                }
            });
```
### 25.ajax在laravel框架中的使用(get方法)

```
function changeOrder(cate_id,obj){
            $.ajax({
                url:"{{url('admin/changeOrder').'/'}}"+cate_id+'/cate_order/'+obj.value,
                type:'get',
                success:function(data){
                    if(data.status==1){
                        layer.msg(data.msg,{icon:6});
                    }else{
                        layer.msg(data.msg,{icon:5});
                    }

                }
            });
        }
```
### 26，不用ajax,怎么在表单中直接提交修改删除这些操作？

```
    <form action="/foo/bar" method="POST">
        <input type="hidden" name="_method" value="PUT">
        <input type="hidden" name="_token" value="{{ csrf_token() }}">
    </form>
```
或者：

```
    {{ method_field('PUT') }}
```
### 27.中间件

HTTP 中间件提供了一个方便的机制来过滤进入应用程序的 HTTP 请求，例如，Auth 中间件验证用户的身份，如果用户未通过身份验证，中间件将会把用户导向登录页面，反之，当用户通过了身份验证，中间件将会通过此请求并接着往下执行。

### 28.创建中间件

```
    php artisan make:middleware AdminLogin
```
新创建的中间件命名空间及方法

```
    namespace App\Http\Middleware;

use Closure;

class AdminLogin
{
    /**
     * Handle an incoming request.
     *
     * @param  \Illuminate\Http\Request  $request
     * @param  \Closure  $next
     * @return mixed
     */
    public function handle($request, Closure $next)
    {
        if(!session('user')){
            return redirect('admin/login');
        }
        return $next($request);
    }
}
```
### 29.注册中间件
在app/Http/Kernel.php的$middleware属性中添加中间件

```
    protected $routeMiddleware = [
        'auth' => \App\Http\Middleware\Authenticate::class,
        'auth.basic' => \Illuminate\Auth\Middleware\AuthenticateWithBasicAuth::class,
        'can' => \Illuminate\Foundation\Http\Middleware\Authorize::class,
        'guest' => \App\Http\Middleware\RedirectIfAuthenticated::class,
        'throttle' => \Illuminate\Routing\Middleware\ThrottleRequests::class,
        'admin.login' => \App\Http\Middleware\AdminLogin::class,
    ];
```

最后一个，就是刚才创建的中间件
### 30.指派中间件

```
    Route::group(['middleware'=>['web','admin.login'],'prefix'=>'admin','namespace'=>'Admin'],function(){
    //后台首页
    Route::get('/index','IndexController@index');
    //退出登录
    Route::get('/quit','LoginController@quit');
    //修改密码
    Route::any('/pass','IndexController@pass');
    //测试方法
    Route::any('/test','IndexController@test');
    //文章分类
    Route::resource('/category','CategoryController');
    //文章管理
    Route::resource('/article','ArticleController');
    //修改分类排序
    Route::get('/changeOrder/{cate_id}/cate_order/{cate_order}','CategoryController@changeOrder');
    //上传图片
    Route::any('/upload','CommonController@upload');
    //文章审核
    Route::get('/shenhe/{art_id}','ArticleController@shenhe');
    //文章上架
    Route::get('/up/{art_id}','ArticleController@up');
    //文章下架
    Route::get('/stop/{art_id}','ArticleController@stop');
    //友情链接
    Route::resource('/links','LinksController');
    //修改友情链接排序
    Route::get('/changeLinkOrder/{link_id}/link_order/{link_order}','LinksController@changeOrder');
    //导航
    Route::resource('/navs','NavsController');
    //修改导航排序
    Route::get('/changeNavOrder/{nav_id}/nav_order/{nav_order}','NavsController@changeOrder');
    //网站配置
    Route::resource('/conf','ConfigController');
    //修改配置顺序
    Route::get('/changeConfOrder/{conf_id}/conf_order/{conf_order}','ConfigController@changeOrder');
    Route::post('/multi_edit','ConfigController@multiEdit');
    Route::get('/gen_conf','ConfigController@putFile');
});
```
以上路由都需要在登录的情况下再能执行
### 31.路由缓存

```
    php artisan route:cache
```
清除缓存路由

```
    php artisan route:clear
```
### 32.获取URL地址

```
    // 不包含请求字串
    $url = $request->url();

    // 包含请求字串（请求字串如：`?id=2`）
    $url = $request->fullUrl();
```
### 33.获取（请求的方法）

```
    $method = $request->method();
```

### 34.判断http动作


```
    if ($request->isMethod('post')) {
        //
    }
```
### 35.获取表单提交数据(Innput类)

```
    $input=Input::except('_token');
    $input=Input::all();
```
### 36.获取表单提交数据(Request)

```
    $name = $request->input('name');
```
或者

```
    $name = $request->name;
```
### 37.确认是否有输入值

```当提交的数据中有字段name且不为空时，
    if ($request->has('name')) {
    //
    }
```
### 38.获取输入数据(Request)

```
    $input = $request->all();
    $input = $request->except('credit_card');
```
### 39.判断是否有文件上传

```
    if ($request->hasFile('photo')) {
    //
    }
```
### 40.获取上传文件

```
    $file = $request->file('photo');
    $file=Input::file('file');
```
### 41.判断上传文件是否有效

```
    if($file->isValid()){

        }
```
### 42.获取上传文件的扩展名

```
     $entension=$file->getClientOriginalExtension();
```
### 43.重定向

```
    Route::get('dashboard', function () {
        return redirect('home/dashboard');
    });
```
### 44.重定向至控制器行为

```
    return redirect()->action('HomeController@index');
```
### 45.使用视图

```
    return view('admin.profile');
```
### 46.判断视图是否存在

```
    if (view()->exists('emails.customer')) {
        //
    }
```
### 47.向视图传数据

```
    return view('greetings', ['name' => 'Victoria']);


    $data=Links::find($id);
     return view('admin.links.edit',compact('data'));
```
### 48.向视图传数据

```
    $category=new Category();
    $data=$category->getTree();
    return view('admin.category.index')->with('data',$data);
```
### 49.数据共享

```
    class CommonController extends Controller
    {
        public function __construct(){
            $nav= Category::orderBy('cate_order','asc')->get();
           View::share('nav',$nav);
        }
    }
```
注意：这个类是个基类，它共享的数据在它的派生类对应的视图中实现。
### 50.Blade模板
Blade 是 Laravel 所提供的一个简单且强大的模板引擎。相较于其它知名的 PHP 模板引擎，Blade 并不会限制你必须得在视图中使用 PHP 代码。所有 Blade 视图都会被编译缓存成普通的 PHP 代码，一直到它们被更改为止。这代表 Blade 基本不会对你的应用程序生成负担。

Blade 视图文件使用 .blade.php 做为扩展名，通常保存于 resources/views 文件夹内。
### 51.模板继承
定义父模板，公共部分留在这里，需要改变的使用yield

```
    <html>
    <head>
        <title>应用程序名称 - @yield('title')</title>
    </head>
    <body>
        @section('sidebar')
            这是主要的侧边栏。
        @show

        <div class="container">
            @yield('content')
        </div>
    </body>
    </html>
```
在子页面中继承

```
    @extends('layouts.master')

    @section('title', '页面标题')

    @section('sidebar')
        @parent

        <p>这边会附加在主要的侧边栏。</p>
    @endsection

    @section('content')
        <p>这是我的主要内容。</p>
    @endsection
```
@parent命令是添加而不是覆盖

### 52.在子模板中改变父级模板内容
首先在父级模板中

```
    @section('title')
    <title>国民的博客</title>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no" />
    @show
```
在子模板中直接更换这个部分。如果子模板中不写这个section，那么模板会默认继承。
### 53.blade数据显示

```
{{ $name }}.
目前的 UNIX 时间戳为 {{ time() }}。
```

### 54.数据存在时输出

```
    {{ $name or 'Default' }}
```
类似于三元操作符
### 55.显示未转义数据

```
 {!! $name !!}.
```
### 56.if表达式

```
    @if (count($records) === 1)
        我有一条记录！
    @elseif (count($records) > 1)
        我有多条记录！
    @else
        我没有任何记录！
    @endif
```
### 57.循环

```
    @for ($i = 0; $i < 10; $i++)
        目前的值为 {{ $i }}
    @endfor

    @foreach ($users as $user)
        <p>此用户为 {{ $user->id }}</p>
    @endforeach

    @forelse ($users as $user)
        <li>{{ $user->name }}</li>
    @empty
        <p>没有用户</p>
    @endforelse

    @while (true)
        <p>我永远都在跑循环。</p>
    @endwhile
```
### 58.目录结构
- app 目录，如你所料，这里面包含应用程序的核心代码。我们之后将很快对这个目录的细节进行深入探讨。

- bootstrap 目录包含了几个框架启动跟自动加载设置的文件。以及在 cache 文件夹中包含着一些框架在启动性能优化时所生成的文件。

- config 目录，顾名思义，包含所有应用程序的配置文件。

- database 目录包含数据库迁移与数据填充文件。如果你愿意的话，你也可以在此文件夹存放 SQLite 数据库。

- public 目录包含了前端控制器和资源文件（图片、JavaScript、CSS，等等）。

- resources 目录包含了视图、原始的资源文件 (LESS、SASS、CoffeeScript) ，以及语言包。

- storage 目录包含编译后的 Blade 模板、基于文件的 session、文件缓存和其它框架生成的文件。此文件夹分格成 app、framework，及 logs 目录。app 目录可用于存储应用程序使用的任何文件。framework 目录被用于保存框架生成的文件及缓存。最后，logs 目录包含了应用程序的日志文件。

- tests 目录包含自动化测试。这有一个现成的 PHPUnit 例子。

- vendor 目录包含你的 Composer 依赖模块。

### 59.加密

```
$user->user_pass=Crypt::encrypt($input['password']);
```
### 60解密

```
$password=Crypt::decrypt($user->user_pass);
```
### 61.日志模式

```
'log' => 'daily'
```
laravel提供四种日志模式

- single
- daily
- syslog
- errorlog

### 62.全部分页

```
$users = DB::table('users')->paginate(15);
```
### 63.上一页、下一页

```
$users = DB::table('users')->simplePaginate(15);
```
### 64.对Eloquent进行分页

```
$users = User::where('votes', '>', 100)->paginate(15);
```
### 65.视图中显示分页

```
{{ $users->links() }
```
### 66.表单验证

```
    $rules=[
        'oldpass'=>'required',
        'password'=>'required|between:6,20|confirmed',
    ];
    $messages=[
        'oldpass.required'=>'旧密码不能为空',
        'password.required'=>'新密码不能为空',
        'password.between'=>'新密码在6-20位之间',
        'password.confirmed'=>'新密码和确认密码不一致',
    ];
    $validator=Validator::make($input,$rules,$messages);
    if($validator->passes()){
        //验证通过，。。
    }else{
        $errors=$validator->errors()->all();
        echo json_encode($errors);
    }
```
### 67.查看特定字段的第一个错误消息

```
$messages = $validator->errors();

echo $messages->first('email');
```
### 68.判断特定字段是否有错误消息

```
if ($messages->has('email')) {
    //
}
```
### 69.可用的验证规则
- accepted
验证字段值是否为 yes、on、1、或 true。这在确认「服务条款」是否同意时相当有用。


- active_url
验证字段值是否为一个有效的网址，会通过 PHP 的 checkdnsrr 函数来验证。
alpha
验证字段值是否仅包含字母字符。


- alpha_dash
验证字段值是否仅包含字母、数字、破折号（ - ）以及下划线（ _ ）。


- alpha_num
验证字段值是否仅包含字母、数字。


- array
验证字段必须是一个 PHP array。
- between:min,max
验证字段值的大小是否介于指定的 min 和 max 之间。字符串、数值或是文件大小的计算方式和 size 规则相同。

- digits:value
验证字段值是否为 numeric 且长度为 value。
- integer
验证字段值是否是整数。
- numeric
验证字段值是否为数值。
70.laravel支持的数据库
- MySQL
- Postgres
- SQLite
- SQL Server

### 71.数据库配置
在config/database.php页面

```
    'mysql' => [
            'driver' => 'mysql',
            'host' => env('DB_HOST', 'localhost'),
            'port' => env('DB_PORT', '3306'),
            'database' => env('DB_DATABASE', 'forge'),
            'username' => env('DB_USERNAME', 'forge'),
            'password' => env('DB_PASSWORD', ''),
            //'prefix' => env('DB_PREFIX', ''),
            'charset' => 'utf8',
            'collation' => 'utf8_unicode_ci',
            'prefix' => '',
            'strict' => false,
            'engine' => null,
        ],
```
### 72.数据库读写分离

```
'mysql' => [
            'read' => [
                'host' => '192.168.1.1',
            ],
            'write' => [
                'host' => '196.168.1.2'
            ],
            'driver' => 'mysql',
            'port' => env('DB_PORT', '3306'),
            'database' => env('DB_DATABASE', 'forge'),
            'username' => env('DB_USERNAME', 'forge'),
            'password' => env('DB_PASSWORD', ''),
            //'prefix' => env('DB_PREFIX', ''),
            'charset' => 'utf8',
            'collation' => 'utf8_unicode_ci',
            'prefix' => '',
            'strict' => false,
            'engine' => null,
        ],
```
### 73.原始SQL查找

```
$users = DB::select('select * from users where active = ?', [1]);
```
DB facade 提供类型的查找方法还有：update、insert、delete、statement。

### 74.使用命名绑定

```
$results = DB::select('select * from users where id = :id', ['id' => 1]);
```
### 75.insert

```
DB::insert('insert into users (id, name) values (?, ?)', [1, 'Dayle']);
```
### 76.update

```
$affected = DB::update('update users set votes = 100 where name = ?', ['John']);
```
### 77.delete

```
$deleted = DB::delete('delete from users');
```
### 78.一般声明

```
DB::statement('drop table users');
```
### 79.结果集中获取所有数据列

```
$users = DB::table('users')->get();
```
### 80.从数据表中获取单个列或者行

```
$user = DB::table('users')->where('name', 'John')->first();

echo $user->name;
```
### 81.获取某个字段值

```
$email = DB::table('users')->where('name', 'John')->value('email');
```
### 82.获取字段值列表

```
$titles = DB::table('roles')->pluck('title');
```
### 83.聚合
查询构造器也提供了各种聚合方法，例如 count、max、min、avg、以及 sum。

```
$users = DB::table('users')->count();

$price = DB::table('orders')->max('price');
```
### 84.select字句

```
$users = DB::table('users')->select('name', 'email as user_email')->get();
```
### 85.Left Join

```
$users = DB::table('users')
            ->leftJoin('posts', 'users.id', '=', 'posts.user_id')
            ->get();
```
### 86.where 字句

```
$users = DB::table('users')->where('votes', '=', 100)->get();
```
上面查询也可以写成这样

```
$users = DB::table('users')->where('votes', 100)->get();
```
### 87.where字句其他算法

```
$users = DB::table('users')
                ->where('votes', '>=', 100)
                ->get();

$users = DB::table('users')
                ->where('votes', '<>', 100)
                ->get();

$users = DB::table('users')
                ->where('name', 'like', 'T%')
                ->get();
```
### 88.orderBy排序

```
$users = DB::table('users')
                ->orderBy('name', 'desc')
                ->get();
```
### 89.获取结果随机排序

```
$randomUser = DB::table('users')
                ->inRandomOrder()
                ->first();
```

### 90.限制查找数量

```
$users = DB::table('users')->skip(10)->take(5)->get();
```
### 91.插入

```
DB::table('users')->insert(
    ['email' => 'john@example.com', 'votes' => 0]
);
```
### 92.更新

```
DB::table('users')
            ->where('id', 1)
            ->update(['votes' => 1]);
```
### 93.删除

```
DB::table('users')->where('votes', '<', 100)->delete();
```
### 94.数据库迁移事可用的字段类型

```

    命令	描述
    $table->bigIncrements('id');	递增 ID（主键），相当于「UNSIGNED BIG INTEGER」型态。
    $table->bigInteger('votes');	相当于 BIGINT 型态。
    $table->binary('data');	相当于 BLOB 型态。
    $table->boolean('confirmed');	相当于 BOOLEAN 型态。
    $table->char('name', 4);	相当于 CHAR 型态，并带有长度。
    $table->date('created_at');	相当于 DATE 型态。
    $table->dateTime('created_at');	相当于 DATETIME 型态。
    $table->dateTimeTz('created_at');	DATETIME (with timezone) 带时区形态
    $table->decimal('amount', 5, 2);	相当于 DECIMAL 型态，并带有精度与基数。
    $table->double('column', 15, 8);	相当于 DOUBLE 型态，总共有 15 位数，在小数点后面有 8 位数。
    $table->enum('choices', ['foo', 'bar']);	相当于 ENUM 型态。
    $table->float('amount');	相当于 FLOAT 型态。
    $table->increments('id');	递增的 ID (主键)，使用相当于「UNSIGNED INTEGER」的型态。
    $table->integer('votes');	相当于 INTEGER 型态。
    $table->ipAddress('visitor');	相当于 IP 地址形态。
    $table->json('options');	相当于 JSON 型态。
    $table->jsonb('options');	相当于 JSONB 型态。
    $table->longText('description');	相当于 LONGTEXT 型态。
    $table->macAddress('device');	相当于 MAC 地址形态。
    $table->mediumInteger('numbers');	相当于 MEDIUMINT 型态。
    $table->mediumText('description');	相当于 MEDIUMTEXT 型态。
    $table->morphs('taggable');	加入整数 taggable_id 与字符串 taggable_type。
    $table->nullableTimestamps();	与 timestamps() 相同，但允许为 NULL。
    $table->rememberToken();	加入 remember_token 并使用 VARCHAR(100) NULL。
    $table->smallInteger('votes');	相当于 SMALLINT 型态。
    $table->softDeletes();	加入 deleted_at 字段用于软删除操作。
    $table->string('email');	相当于 VARCHAR 型态。
    $table->string('name', 100);	相当于 VARCHAR 型态，并带有长度。
    $table->text('description');	相当于 TEXT 型态。
    $table->time('sunrise');	相当于 TIME 型态。
    $table->timeTz('sunrise');	相当于 TIME (with timezone) 带时区形态。
    $table->tinyInteger('numbers');	相当于 TINYINT 型态。
    $table->timestamp('added_on');	相当于 TIMESTAMP 型态。
    $table->timestampTz('added_on');	相当于 TIMESTAMP (with timezone) 带时区形态。
    $table->timestamps();	加入 created_at 和 updated_at 字段。
    $table->uuid('id');	相当于 UUID 型态。
```
### 95.字段修饰

```
    ->first()	将此字段放置在数据表的「第一个」（仅限 MySQL）
    ->after('column')	将此字段放置在其它字段「之后」（仅限 MySQL）
    ->nullable()	此字段允许写入 NULL 值
    ->default($value)	为此字段指定「默认」值
    ->unsigned()	设置 integer 字段为 UNSIGNED
    ->comment('my comment')	增加注释
```
### 96.创建索引

```
$table->string('email')->unique();
```

或者

```
$table->unique('email');
```
### 97.可用的索引类型

```
    $table->primary('id');	加入主键。
    $table->primary(['first', 'last']);	加入复合键。
    $table->unique('email');	加入唯一索引。
    $table->unique('state', 'my_index_name');	自定义索引名称。
    $table->index('state');	加入基本索引。
```
### 98.数据填充命令

```
php artisan make:seeder UsersTableSeeder
```

### 99.运行数据填充

```
php artisan db:seed --class=UserTableSeeder
```
### 100.Eloquent中数据表关联

```
class Flight extends Model
{

    protected $table = 'my_flights';
}
```
### 101.设置表主键 ###

     protected $primaryKey='art_id';

### 102.设置默认时间戳 ###

    public $timestamps=false;

### 103.批量赋值保护 ###

     protected $guarded=[];

### 104.为模型指定不同的链接 ###

    protected $connection = 'connection-name';

### 105.取回多个模型 ###

    $flights = Flight::all();

### 106.增加额外限制 ###

    $flights = App\Flight::where('active', 1)
               ->orderBy('name', 'desc')
               ->take(10)
               ->get();

### 107.通过主键取回一个模型 ###

	$data=Navs::find($id);

### 108.取回符合限制条件的第一个模型 ###

	$flight = App\Flight::where('active', 1)->first();

### 109.抛出未找到异常 ###

	$model = App\Flight::findOrFail(1);
	
	$model = App\Flight::where('legs', '>', 100)->firstOrFail();

在找不到模型时抛出一个异常，如果捕捉到异常，则自动送回http 404响应给用户

### 109.取回集合 ###

	$count = App\Flight::where('active', 1)->count();
	
	$max = App\Flight::where('active', 1)->max('price');

### 110.基本添加 ###

	public function store(Request $request)
    {
        // 验证请求...

        $flight = new Flight;

        $flight->name = $request->name;

        $flight->save();
    }

### 111.基本更新 ###

	$flight = App\Flight::find(1);
	
	$flight->name = 'New Flight Name';
	
	$flight->save()

### 112.批量赋值白名单 ###

	protected $fillable = ['name'];

### 113.删除模型 ###

	$flight = App\Flight::find(1);
	
	$flight->delete();

### 114.通过键删除模型 ###

	App\Flight::destroy(1);
	
	App\Flight::destroy([1, 2, 3]);
	
	App\Flight::destroy(1, 2, 3);

### 115.通过查找删除模型 ###

	$re=Navs::where('nav_id',$id)->delete();

### 116.Eloquent集合 ###

	$users = App\User::where('active', 1)->get();

### 117.Eloquent集合所有方法###

- all
- avg
- chunk
- collapse
- combine
- contains
- count
- diff
- diffKeys
- each
- every
- except
- filter
- first
- flatMap
- flatten
- flip
- forget
- forPage
- get
- groupBy
- has
- implode
- intersect
- isEmpty
- keyBy
- keys
- last
- map
- max
- merge
- min
- only
- pluck
- pop
- prepend
- pull
- push
- put
- random
- reduce
- reject
- reverse
- search
- shift
- shuffle
- slice
- sort
- sortBy
- sortByDesc
- splice
- sum
- take
- toArray
- toJson
- transform
- union
- unique
- values
- where
- whereLoose
- whereIn
- whereInLoose
- zip


### 118.集合对象-map ###

	$data=Links::orderBy('link_order','asc')->get();
    $names=$data->map(function($name){
        return $name->link_name;
    });
    dd($names);

输出

	Collection {#245 ▼
	  #items: array:3 [▼
	    0 => "百度"
	    1 => "雅虎"
	    2 => "google"
	  ]
	}

### 119.集合对象-all(所有) ###

	$data=Links::orderBy('link_order','asc')->get();
    $names=$data->all(function($name){
        return $name->link_name;
    });
    dd($names);

输出

	array:3 [▼
	  0 => Links {#258 ▶}
	  1 => Links {#259 ▶}
	  2 => Links {#260 ▶}
	]

### 120.集合对象-avg(平均值) ###

	$data=Links::orderBy('link_order','asc')->get();
    $names=$data->avg(function($name){
        return $name->link_order;
    });
    dd($names);

### 121.集合对象-chunk(将集合拆成多个指定大小的较小集合) ###

	$names=$data->chunk(3);
    dd($names->toArray());

输出

	array:5 [▼
	  0 => array:3 [▶]
	  1 => array:3 [▶]
	  2 => array:3 [▶]
	  3 => array:3 [▶]
	  4 => array:1 [▶]
	]

这个方法适用于网格系统如Bootstrap的视图

	@foreach ($products->chunk(3) as $chunk)
	    <div class="row">
	        @foreach ($chunk as $product)
	            <div class="col-xs-4">{{ $product->name }}</div>
	        @endforeach
	    </div>
	@endforeach

### 122.集合对象-collapse(将多个数组组成的集合合成单个数组集合) ###

	$collection = collect([[1, 2, 3], [4, 5, 6], [7, 8, 9]]);

    $collapsed = $collection->collapse();

    dd($collapsed->all());

输出

	array:9 [▼
	  0 => 1
	  1 => 2
	  2 => 3
	  3 => 4
	  4 => 5
	  5 => 6
	  6 => 7
	  7 => 8
	  8 => 9
	]

### 123.集合对象-combine(将集合的值作为键，合并另一个数组或者集合作为键对应的值) ###

对应英文：The combine method combines the keys of the collection with the values of another array or collection:

	$collection = collect(['name', 'age']);
	
	$combined = $collection->combine(['George', 29]);
	
	$combined->all();

输出

	array:2 [▼
	  "name" => "George"
	  "age" => 29
	]

### 124.集合对象-contains(判断集合是否含有指定项目) ###

	$collection = collect(['name' => 'Desk', 'price' => 100]);
	
	$collection->contains('Desk');

输出

	true

### 125.集合对象count(项目总数) ###

	$data=Links::orderBy('link_order','asc')->get();
    $contains=$data->count();

    dd($contains);

### 126.集合对象-diff(将集合与其他集合或者php数组比较) ###



	$collection = collect([1, 2, 3, 4, 5]);
	
	$diff = $collection->diff([2, 4, 6, 8]);
	
	$diff->all();


### 127.集合对象-each(遍历集合中的项目，并将之传入回调函数) ###

	$collection = $collection->each(function ($item, $key) {
	    //
	});

### 128.集合对象-every(创建每包含第n个元素的新集合) ###

	$collection = collect(['a', 'b', 'c', 'd', 'e', 'f']);
	
	$collection->every(4);

输出

	Collection {#245 ▼
	  #items: array:2 [▼
	    0 => "a"
	    1 => "e"
	  ]
	}

### 129.集合对象-except(返回集合中除了指定键的所有项目) ###

	$collection = collect(['product_id' => 1, 'name' => 'Desk', 'price' => 100, 'discount' => false]);
	
	$filtered = $collection->except(['price', 'discount']);
	
	$filtered->all();

输出

	['product_id' => 1, 'name' => 'Desk']

### 130.集合对象-filter(使用回调函数筛选集合，只留下通过判断测试的项目) ###

	$collection = collect([1, 2, 3, 4]);
	
	$filtered = $collection->filter(function ($item) {
	    return $item > 2;
	});
	
	$filtered->all();

### 131.集合对象first(返回集合第一个通过制定测试的元素) ###

	$data=Links::orderBy('link_order','asc')->first();
    dd($data);

输出
	
    Links {#256 ▼
	  #table: "links"
	  #primaryKey: "link_id"
	  +timestamps: false
	  #guarded: []
	  #connection: null
	  #keyType: "int"
	  #perPage: 15
	  +incrementing: true
	  #attributes: array:5 [▶]
	  #original: array:5 [▶]
	  #relations: []
	  #hidden: []
	  #visible: []
	  #appends: []
	  #fillable: []
	  #dates: []
	  #dateFormat: null
	  #casts: []
	  #touches: []
	  #observables: []
	  #with: []
	  #morphClass: null
	  +exists: true
	  +wasRecentlyCreated: false
	}

### 132.集合对象-flatten（将多维集合转为一维集合） ###

	$collection = collect(['name' => 'taylor', 'languages' => ['php', 'javascript']]);
	
	$flattened = $collection->flatten();
	
	$flattened->all();

### 133.集合对象-flip（将集合中的键和对应的值进行互换) ###

	$collection = collect(['name' => 'taylor', 'framework' => 'laravel']);
	
	$flipped = $collection->flip();
	
	dd($flipped->all());

输出

	array:2 [▼
	  "taylor" => "name"
	  "laravel" => "framework"
	]

### 134.通过集合的键来移除集合中的一个项目 ###

	$collection = collect(['name' => 'taylor', 'framework' => 'laravel']);
	
	$collection->forget('name');
	
	$collection->all();

输出

	[framework' => 'laravel']


> 注意：与大多数其它集合的方法不同，forget 不会返回修改过后的新集合；它会直接修改调用它的集合。

### 135.集合对象-has(检查集合中是否含有指定的键) ###

	$collection = collect(['account_id' => 1, 'product' => 'Desk']);
	
	$collection->has('email');

### 136.集合对象-implode(合并集合中的项目) ###

	$collection = collect([
	    ['account_id' => 1, 'product' => 'Desk'],
	    ['account_id' => 2, 'product' => 'Chair'],
	]);
	
	$collection->implode('product', ', ');

输出

	Desk, Chair

或者

	collect([1, 2, 3, 4, 5])->implode('-');

输出

	'1-2-3-4-5'

### 137.集合对象-intersect(移除任何指定数组或者集合内没有的数值) ###

	$collection = collect(['Desk', 'Sofa', 'Chair']);
	
	$intersect = $collection->intersect(['Desk', 'Chair', 'Bookcase']);
	
	$intersect->all();

输出

	[0 => 'Desk', 2 => 'Chair']

相当于去交集

### 138.集合对象-last(返回集合中，最后一个通过指定测试的元素) ###

	$data=Links::orderBy('link_order','asc')->get();
	$keys=$data->last(function($key,$value){
	    return $key<4;
	});
	dd($keys);

### 139.集合对象-max(计算指定键的最大值) ###

	$data=Links::orderBy('link_order','asc')->get();
	$max=$data->max();
	dd($max);

输出最大键对应的结果

### 140.集合对象-only(返回集合中指定键的所有项目) ###

	$collection = collect(['product_id' => 1, 'name' => 'Desk', 'price' => 100, 'discount' => false]);
	
	$filtered = $collection->only(['product_id', 'name']);
	
	$filtered->all();

输出

	['product_id' => 1, 'name' => 'Desk']

### 141.集合对象-pluck(获取所有集合中指定键对应的值) ###

	$data=Links::orderBy('link_order','asc')->get();
	$max=$data->pluck('link_name','link_id');
	dd($max);

输出

	Collection {#245 ▼
	  #items: array:13 [▼
	    6 => "百度"
	    8 => "百度1"
	    10 => "百度2"
	    12 => "百度3"
	    14 => "百度4"
	    1 => "百度"
	    4 => "雅虎"
	    7 => "google"
	    9 => "google1"
	    11 => "google2"
	    13 => "google3"
	    15 => "google4"
	    2 => "google"
	  ]
	}

### 142.集合对象-pop(移除并返回集合最后一个项目) ###

	$collection = collect([1, 2, 3, 4, 5]);
	
	$collection->pop();

	$collection->all();

输出
	
 	[1, 2, 3, 4]
### 143.集合对象-prepend(集合前面添加一个项目) ###

	$data=Links::orderBy('link_order','asc')->get();
    $max=$data->prepend(0);
    dd($data);

输出

	Collection {#267 ▼
	  #items: array:14 [▼
	    0 => 0
	    1 => Links {#268 ▶}
	    2 => Links {#269 ▶}
	    3 => Links {#270 ▶}
	    4 => Links {#271 ▶}
	    5 => Links {#272 ▶}
	    6 => Links {#273 ▶}
	    7 => Links {#274 ▶}
	    8 => Links {#275 ▶}
	    9 => Links {#276 ▶}
	    10 => Links {#277 ▶}
	    11 => Links {#278 ▶}
	    12 => Links {#279 ▶}
	    13 => Links {#280 ▶}
	  ]
	}

也可以传递第二个参数，指定这个值对应的键

	$data=Links::orderBy('link_order','asc')->get();
    $max=$data->prepend(0,'aaa');
    dd($data);

输出

	Collection {#267 ▼
	  #items: array:14 [▼
	    "aaa" => 0
	    0 => Links {#268 ▶}
	    1 => Links {#269 ▶}
	    2 => Links {#270 ▶}
	    3 => Links {#271 ▶}
	    4 => Links {#272 ▶}
	    5 => Links {#273 ▶}
	    6 => Links {#274 ▶}
	    7 => Links {#275 ▶}
	    8 => Links {#276 ▶}
	    9 => Links {#277 ▶}
	    10 => Links {#278 ▶}
	    11 => Links {#279 ▶}
	    12 => Links {#280 ▶}
	  ]
	}

### 144.集合对象-pull(把键对应的值从集合中移除并返回) ###

	$data=Links::orderBy('link_order','asc')->get();
    $max=$data->pull(5);
    dd($data);

输出

	Collection {#267 ▼
	  #items: array:12 [▼
	    0 => Links {#268 ▶}
	    1 => Links {#269 ▶}
	    2 => Links {#270 ▶}
	    3 => Links {#271 ▶}
	    4 => Links {#272 ▶}
	    6 => Links {#274 ▶}
	    7 => Links {#275 ▶}
	    8 => Links {#276 ▶}
	    9 => Links {#277 ▶}
	    10 => Links {#278 ▶}
	    11 => Links {#279 ▶}
	    12 => Links {#280 ▶}
	  ]
	}

### 145.集合对象push(在集合后面添加一个元素) ###

	$data=Links::orderBy('link_order','asc')->get();
    $max=$data->push(5);
    dd($data);

输出

	Collection {#267 ▼
	  #items: array:14 [▼
	    0 => Links {#268 ▶}
	    1 => Links {#269 ▶}
	    2 => Links {#270 ▶}
	    3 => Links {#271 ▶}
	    4 => Links {#272 ▶}
	    5 => Links {#273 ▶}
	    6 => Links {#274 ▶}
	    7 => Links {#275 ▶}
	    8 => Links {#276 ▶}
	    9 => Links {#277 ▶}
	    10 => Links {#278 ▶}
	    11 => Links {#279 ▶}
	    12 => Links {#280 ▶}
	    13 => 5
	  ]
	}

### 146.集合对象-put(在集合内设置一个键值) ###

	$data=Links::orderBy('link_order','asc')->get();
    $max=$data->put('aa','bbb');
    dd($data);
输出

	Collection {#267 ▼
	  #items: array:14 [▼
	    0 => Links {#268 ▶}
	    1 => Links {#269 ▶}
	    2 => Links {#270 ▶}
	    3 => Links {#271 ▶}
	    4 => Links {#272 ▶}
	    5 => Links {#273 ▶}
	    6 => Links {#274 ▶}
	    7 => Links {#275 ▶}
	    8 => Links {#276 ▶}
	    9 => Links {#277 ▶}
	    10 => Links {#278 ▶}
	    11 => Links {#279 ▶}
	    12 => Links {#280 ▶}
	    "aa" => "bbb"
	  ]
	}

也可以更换已有键的值

	$data=Links::orderBy('link_order','asc')->get();
    $max=$data->put(5,'bbb');
    dd($data);

输出

	Collection {#267 ▼
	  #items: array:13 [▼
	    0 => Links {#268 ▶}
	    1 => Links {#269 ▶}
	    2 => Links {#270 ▶}
	    3 => Links {#271 ▶}
	    4 => Links {#272 ▶}
	    5 => "bbb"
	    6 => Links {#274 ▶}
	    7 => Links {#275 ▶}
	    8 => Links {#276 ▶}
	    9 => Links {#277 ▶}
	    10 => Links {#278 ▶}
	    11 => Links {#279 ▶}
	    12 => Links {#280 ▶}
	  ]
	}

### 147.集合对象-random(从集合中随机取出一个项目) ###

	$data=Links::orderBy('link_order','asc')->get();
    $max=$data->random();
    dd($max);

输出

	Links {#275 ▼
	  #table: "links"
	  #primaryKey: "link_id"
	  +timestamps: false
	  #guarded: []
	  #connection: null
	  #keyType: "int"
	  #perPage: 15
	  +incrementing: true
	  #attributes: array:5 [▶]
	  #original: array:5 [▶]
	  #relations: []
	  #hidden: []
	  #visible: []
	  #appends: []
	  #fillable: []
	  #dates: []
	  #dateFormat: null
	  #casts: []
	  #touches: []
	  #observables: []
	  #with: []
	  #morphClass: null
	  +exists: true
	  +wasRecentlyCreated: false
	}

### 147.集合对象-reduce(将集合缩缩减到单个数值，该方法将每次迭代的结果传入到下一次迭代) ###

	$collection = collect([1, 2, 3]);
	
	$total = $collection->reduce(function ($carry, $item) {
	    return $carry + $item;
	});

输出

	6

### 148.集合对象-reject(以指定的回调函数筛选集合，该回调函数应该对希望从最终集合移除掉的项目返回true) ###

	$collection = collect([1, 2, 3, 4]);
	
	$filtered = $collection->reject(function ($item) {
	    return $item > 2;
	});
	
	$filtered->all();

输出

	[1, 2]

### 148.集合对象-reverse(倒转集合内项目的顺序) ###

	$collection = collect([1, 2, 3, 4, 5]);
	
	$reversed = $collection->reverse();
	
	$reversed->all();

输出

	[5, 4, 3, 2, 1]

### 149.集合对象-shift(移除并返回集合的第一个项目) ###

	$data=Links::orderBy('link_order','asc')->get();
    $total = $data->shift();
    dd($data);

输出

	Collection {#267 ▼
	  #items: array:12 [▼
	    0 => Links {#269 ▶}
	    1 => Links {#270 ▶}
	    2 => Links {#271 ▶}
	    3 => Links {#272 ▶}
	    4 => Links {#273 ▶}
	    5 => Links {#274 ▶}
	    6 => Links {#275 ▶}
	    7 => Links {#276 ▶}
	    8 => Links {#277 ▶}
	    9 => Links {#278 ▶}
	    10 => Links {#279 ▶}
	    11 => Links {#280 ▶}
	  ]
	}


### 150.集合对象-slice(返回集合从指定索引开始的一部分切片) ###

	$data=Links::orderBy('link_order','asc')->get();
    $total = $data->slice(4);
    dd($total);

输出

	Collection {#252 ▼
	  #items: array:9 [▼
	    4 => Links {#272 ▶}
	    5 => Links {#273 ▶}
	    6 => Links {#274 ▶}
	    7 => Links {#275 ▶}
	    8 => Links {#276 ▶}
	    9 => Links {#277 ▶}
	    10 => Links {#278 ▶}
	    11 => Links {#279 ▶}
	    12 => Links {#280 ▶}
	  ]
	}

### 151.集合对象-splice(返回指定的索引开始的一小切片项目，原本的集合也会被删除) ###

	$collection = collect([1, 2, 3, 4, 5]);
	
	$chunk = $collection->splice(2);
	
	$chunk->all();

输出

	// [3, 4, 5]

原来的集合被切除

	$collection = collect([1, 2, 3, 4, 5]);
	
	$chunk = $collection->splice(2);
	
	$collection->all();

输出

	// [1, 2]

### 152.集合对象-sum(返回集合内所有项目的总和) ###

	collect([1, 2, 3, 4, 5])->sum();

输出

	15

### 153.集合对象-take(返回有着指定数量项目的集合) ###

	$collection = collect([0, 1, 2, 3, 4, 5]);
	
	$chunk = $collection->take(3);
	
	$chunk->all();

输出

	[0, 1, 2]

也可以传入负数获取从集合后面来算指定数量的项目

	$collection = collect([0, 1, 2, 3, 4, 5]);
	
	$chunk = $collection->take(-2);
	
	$chunk->all();
	

输出  

	// [4, 5]

### 154.集合对象-toArray(将集合转换成纯php数组) ###

	$data=Links::orderBy('link_order','asc')->get();
    $total = $data->toArray();
    dd($total);

输出

	array:13 [▼
	  0 => array:5 [▼
	    "link_id" => 6
	    "link_name" => "百度"
	    "link_title" => "全球最大的中文搜索引擎"
	    "link_url" => "https://www.baidu.com"
	    "link_order" => 1
	  ]
	  1 => array:5 [▶]
	  2 => array:5 [▶]
	  3 => array:5 [▶]
	  4 => array:5 [▶]
	  5 => array:5 [▶]
	  6 => array:5 [▶]
	  7 => array:5 [▶]
	  8 => array:5 [▶]
	  9 => array:5 [▶]
	  10 => array:5 [▶]
	  11 => array:5 [▶]
	  12 => array:5 [▶]
	]

### 155.集合对象-toJSON（将集合转换成json） ###

	$collection = collect(['name' => 'Desk', 'price' => 200]);
	
	$collection->toJson();

输出

	'{"name":"Desk","price":200}'

### 156.集合对象-zip(将集合与指定数组同样索引的值合并在一起) ###

	$collection = collect(['Chair', 'Desk']);
	
	$zipped = $collection->zip([100, 200]);
	
	$zipped->all();

输出

	[['Chair', 100], ['Desk', 200]]

### 157.设置session函数 ###

	session(['user'=>$user]);

### 158.销毁这个session ###

	session(['user'=>'']);

### 159.模板引入css和js ###

	<script type="text/javascript" src="{{asset('resources/views/admin/lib/html5.js')}}"></script>

### 160.模板页面书写url ###

	{{url('admin/code')}}

## 一、把本地项目上传到git远程仓库 ##
### 1.初始化项目 ###

	git init

### 2.文件添加到版本库 ###

	git add .

### 3.文件提交到仓库 ###

	git commit -m "文件提交"

### 4.关联远程仓库 ###

	git remote add origin git@github.com:yushi5344/vueJs.git

### 5.获取远程库与本地合并 ###

	git pull --rebase origin master

### 6.把本地库推送到远程 ###

	git push -u origin master


## 二、将项目复制到新环境 ##

### 1.先进行克隆 ###

	git clone git@github.com:yushi5344/vueJs.git

### 2.解决依赖 ###

	composer install

### 3.建立.env文件 ###

	cp .env.example .env

### 4.生成key ###

	php artisan key:generate

### 5.在env文件中设置响应数据库信息 ###

	APP_ENV=local
	APP_KEY=base64:H6RIhyLBY-SOME-KEY-HERE-FkzCvGdS8WOU=
	APP_DEBUG=true
	APP_LOG_LEVEL=debug
	APP_URL=http://localhost
	
	DB_CONNECTION=mysql
	DB_HOST=127.0.0.1
	DB_PORT=3306
	DB_DATABASE=my_dbname
	DB_USERNAME=homestead
	DB_PASSWORD=secret

### 6.建立数据库 ###

	php artisan migrate

## 三、可能遇到的问题 ##

### 1.linux上没有安装git  ###

	yum install git 

### 2.linux上没有安装composer ###

1. 下载composer

		curl -sS https://getcomposer.org/installer | php
1. 将composer.phar文件移动到bin目录，全局使用composer命令

		mv composer.phar /usr/local/bin/composer

1. 切换国内源

		composer config -g repo.packagist composer https://packagist.phpcomposer.com

### 3.安装依赖报错 ###

	The Process class relies on proc_open,which is not avaliable on your PHP installation

或者

	proc_get_status() has been disabled for security reasons

解决方法

	修改php.ini 配置文件

### 4.首页一片空白，也不报错 ###

	修改storage以及它下面的文件夹权限
	chmod 777 -R storage

### 5.首页可刷出来，其他页面报404错误 ###

	修改nginx.conf文件
	location / {
	    try_files $uri $uri/ /index.php?$query_string;
	}