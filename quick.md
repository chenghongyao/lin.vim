# TODO
- 将切换tab映射为alt+HJKL??


# 其他


- `<leader>c`、`<leader>p`：复制粘贴（在不同的vim中）
- `<leader>c<space>`：注释
- `<space>`：折叠块（函数）
- `<c-p>`：搜索文件




# 窗口
- `<leader>w`：下一个窗口
- `<leader>q`:全部保存并关闭
- `<leader>Q`:不保存关闭所有
- `<leader>f`：跳转到Nerdtree
- `<F1>`：关闭打开Nerdtree

# 自动补全（LSP）
- <c-k>：触发补全列表

# 跳转定义
- `gd`：跳转到定义
- `gy`：跳转到类型定义
- `gi`：跳转到实现
- `gr`：跳转到引用

# Nerdtree
- `?`：切换quickhelp页面
- 文件节点
  - o：打开文件（光标跳转到编辑区）
  - go：预览（打开但不跳转到编辑区）
  - t：在新Tab里打开
  - T: 在新Tab里后台打开
  - i：分栏打开
  - s：垂直分栏打开
  - gi:分栏打开但不跳转
  - gs：垂直分栏打开但不跳转
  - <CR>: 自定义打开
- 目录节点
  - o：展开折叠节点
  - O：递归展开所有子节点
  - t：在新Tab打开(所选节点设置为根节点)
  - T：在新Tab打开但不跳转
  - <CR>：自定义打开
  - x：折叠父节点(并将光标移动到父节点)
  - X：递归折叠当前节点的所有子节点(不包括当前节点)
  - e：探索节点（在编辑区打开）
- 书签表格？
  - TODO
- 树导航
  - P：到根节点
  - p：到父节点
  - K：到第kk一个子节点
  - J：到最后一个子节点
  - <C-j>：到下一个兄弟节点
  - <C-k>：到上一个兄弟节点
- 文件系统
  - C：将根目录设置为所选目录
  - u：将根目录设置为上一级目录
  - U：将根目录设置为上一级目录,并保持当前目录打开
  - r：更新当前根目录(输入两次才能正常显示图标？)
  - m：显示菜单
  - cd：将当前路径设置为当前根目录路径
  - CD：将当前根目录设置为当前路径
- 菜单
  - ma：添加一个文件或文件夹
  - mm：移动当前节点（可用于重命名）
  - md：删除当前节点
  - mc：复制当前节点
  - mp：显示当前节点的绝对路径
  - ml：列出当前节点(看节点的属性)
  - ms：在当前路径下运行系统命令


## asyncrun
[官方](https://github.com/skywind3000/asyncrun.vim/blob/master/README-cn.md)

异步运行单条命令，并将结果输出到quickfix窗口(先用copen打开),格式

```
:AsyncRun[!] [options] {cmd} ...
```
- 在后台运行 shell 命令，并把结果实时输出到 quickfix 窗口，当命令后跟随一个 ! 时，quickfix 将不会自动滚动。
- 参数用空格分隔，如果某项参数包含空格，那么需要双引号引起来（unix 下面还可以使用反斜杠加空格）。
- 特殊宏
```
%:p     - 当前 buffer 的文件名全路径
%:t     - 当前 buffer 的文件名（没有前面的路径）
%:p:h   - 当前 buffer 的文件所在路径
%:e     - 当前 buffer 的扩展名
%:t:r   - 当前 buffer 的主文件名（没有前面路径和后面扩展名）
%       - 相对于当前路径的文件名
%:h:.   - 相对于当前路径的文件路径
<cwd>   - 当前路径
<cword> - 光标下的单词
<cfile> - 光标下的文件名
<root>  - 当前 buffer 的项目根目录
```
- 运行前的环境变量
```
$VIM_FILEPATH  - 当前 buffer 的文件名全路径
$VIM_FILENAME  - 当前 buffer 的文件名（没有前面的路径）
$VIM_FILEDIR   - 当前 buffer 的文件所在路径
$VIM_FILEEXT   - 当前 buffer 的扩展名
$VIM_FILENOEXT - 当前 buffer 的主文件名（没有前面路径和后面扩展名）
$VIM_PATHNOEXT - 带路径的主文件名（$VIM_FILEPATH 去掉扩展名）
$VIM_CWD       - 当前 Vim 目录
$VIM_RELDIR    - 相对于当前路径的文件名
$VIM_RELNAME   - 相对于当前路径的文件路径
$VIM_ROOT      - 当前 buffer 的项目根目录
$VIM_CWORD     - 光标下的单词
$VIM_CFILE     - 光标下的文件名
$VIM_GUI       - 是否在 GUI 下面运行？
$VIM_VERSION   - Vim 版本号
$VIM_COLUMNS   - 当前屏幕宽度
$VIM_LINES     - 当前屏幕高度
$VIM_SVRNAME   - v:servername 的值
```
- 命令参数
| 参数 | 默认值 | 含义 |
|-|-|-|
| `-mode=?` | "async" | 用 `-mode=?` 的形式指定运行模式可选模式有： `"async"` (默认模式，后台运行输出到 quickfix), `"bang"` (使用 `!` 命令运行) 以及 `"terminal"` (在内建终端运行)， 具体查看 [运行模式](#运行模式)。 |
| `-cwd=?` | `未设置` | 命令初始目录（没有设置就用 vim 当前目录），比如  `-cwd=<root>` 就能在 [项目根目录](#项目根目录) 运行命令，或者 `-cwd=$(VIM_FILEDIR)` 就能在当前文件所在目录运行命令。 |
| `-save=?` | 0 | 运行命令前是否保存文件，`-save=1` 保存当前文件，`-save=2` 保存所有修改过的文件 |
| `-program=?` | `未设置` | 设置成 `make` 可以用 `&makeprg`，设置成 `grep` 可以使用 `&grepprt`，而设置成 `wsl` 则可以在 WSL 中运行命令 （需要 Windows 10）|
| `-post=?` | `未设置` | 命令结束后自动运行的 vimscript，如果包含空格则要用反斜杠加空格代替。 |
| `-auto=?` | `未设置` | 出发 autocmd `QuickFixCmdPre`/`QuickFixCmdPost` 后面的名称。 |
| `-raw` | `未设置` | 如果提供了，就输出原始内容，忽略 `&errorformat` 过滤。 |
| `-strip` | `未设置` | 过滤收尾消息 (头部命令名称以及尾部 "[Finished in ...]" 信息)。|
| `-pos=?` | "bottom" | 当用 `-mode=term` 在内置终端运行命令时， `-pos` 用于指定内置终端窗口位置， 可以设置成 `"tab"`，`"curwin"`，`"top"`，`"bottom"`，`"left"` ，`"right"` 和 `"external"`。|
| `-rows=num` | 0 | 内置终端窗口的高度。|
| `-cols=num` | 0 | 内置终端窗口的宽度。|
| `-errorformat=?` | `未设置` | 用于 quickfix 中匹配错误输出的格式字符串，如果未提供，则使用当前 `&errorformat` 的值。注意 `%` 需要转写成 `\%`。 |
| `-focus=?` | 1 | 设置成 `0` 可以防止使用内置终端时窗口焦点切换。 |
| `-hidden=?` | 0 | 设置成 `1` 可以将内置终端的 `bufhidden` 初始化为 `hide` |
- 停止运行
```bash
:AsyncStop[!]
```
- 示例
```
:AsyncRun make
:AsyncRun g++ -O3 "%" -o "%<"
```
- 绑定
```
:noremap <F7> :AsyncRun gcc "$(VIM_FILEPATH)" -o "$(VIM_FILEDIR)/$(VIM_FILENAME)" <cr> 
```
> 使用 -raw 参数可以在 quickfix 中显示原始输出（不进行 errorformat 匹配），记得用 let $PYTHONNUNBUFFERED=1 来禁止 python 的行缓存，这样可以实时查看结果。很多程序在后台运行时都会将输出全部缓存住直到调用 flush 或者程序结束，python 可以设置该变量来禁用缓存，让你实时看到输出，而无需每次手工调用 sys.stdout.flush()。

```bash
:AsyncRun -raw python %
```


- 
## asynctask
- 项目配置：`*.task`
- 全局配置：`~\.vim\tasks.ini`

# vim-terminal-help
