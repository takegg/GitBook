# webpack

# <a href="https://webpack.docschina.org/concepts/">中文文档</a>
# <a href="https://webpack.toobug.net/zh-cn/">webpack指南</a>

### webpack-cli 参数
```shell
Usage: webpack-cli [options]
       webpack-cli [options] --entry <entry> --output <output>
       webpack-cli [options] <entries...> --output <output>
       webpack-cli <command> [options]

For more information, see https://webpack.js.org/api/cli/.

Config options:
  --config               配置文件，[string] [默认: webpack.config.js 或 webpackfile.js]
  --config-register, -r  在加载webpack配置之前预加载一个或多个模块       [Array] [default: module id or path]
  --config-name          要使用的配置的名称                             [string]
  --env                  当它是一个函数时，环境传递给配置
  --mode                 启用生产优化或开发提示。[选项: "development", "production", "none"]

基础选项:
  --context    用于解析`entry`选项的基础目录（绝对路径！）。 如果设置了`output.pathinfo`，则包含的路径信息缩短为该目录。[string] [默认: 当前目录]
  --entry      编译的入口点.                                            [string]
  --watch, -w  进入监听模式, 在变更的文件上重建.                          [boolean]
  --debug      切换加载器到debug模式                                     [boolean]
  --devtool    一个开发工具以加强debugging.                              [string]
  -d           --debug --devtool eval-cheap-module-source-map --output-pathinfo的快捷方式                                       [boolean]
  -p           --optimize-minimize --define\process.env.NODE_ENV="production"的快捷方式                                         [boolean]
  --progress   以百分比方式打印编译进度                                   [boolean]

模块选项:
  --module-bind       绑定一个扩展到一个加载器                            [string]
  --module-bind-post  绑定一个扩展到一个post加载器                        [string]
  --module-bind-pre   绑定一个扩展到一个pre加载器                         [string]

输出选项:
  --output, -o                  编译资源的输出路径和文件
  --output-path                 以绝对路径输出目录（必须的）。                                                   [string] [默认:当前目录]
  --output-filename             指定每个输出文件在磁盘上的名称。你这里一定不要指定绝对路径！`output.path`选项决定了在磁盘上文件将要写入的位置，filename仅用于命名单个文件。[string] [默认: [name].js]
  --output-chunk-filename       无入口chunks的filename作为`output.path`目录内的相对路径。[string] [默认: filename 以[id]代替[name]或[id]前缀]
  --output-source-map-filename  JavaScript文件的SourceMaps的文件名。 它们位于`output.path`目录中。               [string]
  --output-public-path          `publicPath`指定在浏览器中引用时输出文件的公共URL地址。                           [string]
  --output-jsonp-function       Webpack用于异步加载块的JSONP函数。                                              [string]
  --output-pathinfo             包含有关模块信息的注释。                                                        [boolean]
  --output-library              将入口点导出为库并暴露出来                                                       [string]
  --output-library-target       库类型  [string] [可选择: "var", "assign", "this", "window", "self", "global", "commonjs", "commonjs2", "commonjs-module", "amd", "umd", "umd2", "jsonp"]

高级选项:
  --records-input-path       存储编译状态到json文件                                                         [string]
  --records-output-path      从json文件加载编译器状态。                                                     [string]
  --records-path             从/向json文件存储/加载编译器状态。 这将导致模块和块的持久ID。 预计绝对路径。 `recordsPath`用于`recordsInputPath`和`recordsOutputPath`，如果它们未定义的话。[string]
  --define                   定义bundle中的任何空闲var                                                      [string]
  --target                   用于编译的环境                                                                 [string]
  --cache                    缓存生成的模块和块以提高多个增量构建的性能。[default: 当监听时它默认启动]           [boolean] 
  --watch-stdin, --stdin     当stdin流结束时停止监听                                                         [boolean]
  --watch-aggregate-timeout  在第一次更改后延迟重建。 值是以ms为单位的时间。                                   [number]
  --watch-poll               启用轮询模式以监听                                                              [string]
  --hot                      启用模块热更新                                                                  [boolean]
  --prefetch                 与读取此请求 (Example: --prefetch./file.js)                                     [string]
  --provide                  在所有模块中将这些模块作为自由变量提供 (Example: --provide jQuery=jquery)         [string]
  --labeled-modules          启用带标签的模块                                                                [boolean]
  --plugin                   加载插件                                                                       [string]
  --bail                     将第一个错误报告为硬错误而不是容忍它。[default: null]                             [boolean] 
  --profile                  捕获每个模块的定时信息。 [boolean]  [default: null]

分解选项:
  --resolve-alias         重定向模块请求                      [string]
  --resolve-extensions    重定向模块请求                       [array]
  --resolve-loader-alias  设置加载程序别名以进行解析            [string]

优化选项:
  --optimize-max-chunks      尽量保持块数低于限制
  --optimize-min-chunk-size  创建的块的最小尺寸
  --optimize-minimize        启用最小化输出。 使用optimization.minimizer。                   [boolean]

统计选项:
  --color, --colors               Enables/Disables colors on the console
                                           [boolean] [default: (supports-color)]
  --sort-modules-by               Sorts the modules list by property in module
                                                                        [string]
  --sort-chunks-by                Sorts the chunks list by property in chunk
                                                                        [string]
  --sort-assets-by                Sorts the assets list by property in asset
                                                                        [string]
  --hide-modules                  Hides info about modules             [boolean]
  --display-exclude               Exclude modules in the output         [string]
  --display-modules               Display even excluded modules in the output
                                                                       [boolean]
  --display-max-modules           Sets the maximum number of visible modules in
                                  output                                [number]
  --display-chunks                Display chunks in the output         [boolean]
  --display-entrypoints           Display entry points in the output   [boolean]
  --display-origins               Display origins of chunks in the output
                                                                       [boolean]
  --display-cached                Display also cached modules in the output
                                                                       [boolean]
  --display-cached-assets         Display also cached assets in the output
                                                                       [boolean]
  --display-reasons               Display reasons about module inclusion in the
                                  output                               [boolean]
  --display-depth                 Display distance from entry point for each
                                  module                               [boolean]
  --display-used-exports          Display information about used exports in
                                  modules (Tree Shaking)               [boolean]
  --display-provided-exports      Display information about exports provided
                                  from modules                         [boolean]
  --display-optimization-bailout  Display information about why optimization
                                  bailed out for modules               [boolean]
  --display-error-details         Display details about errors         [boolean]
  --display                       Select display preset
              [string] [choices: "", "verbose", "detailed", "normal", "minimal",
                                                          "errors-only", "none"]
  --verbose                       Show more details                    [boolean]
  --info-verbosity                Controls the output of lifecycle messaging
                                  e.g. Started watching files...
                 [string] [choices: "none", "info", "verbose"] [default: "info"]
  --build-delimiter               Display custom text after build output[string]

Options:
  --help, -h     Show help                                             [boolean]
  --version, -v  Show version number                                   [boolean]
  --silent       防止输出显示在stdout中                                 [boolean]
  --json, -j     将结果打印为JSON。                                     [boolean]
  ```



  