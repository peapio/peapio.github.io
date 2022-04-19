#  介绍一下我的neovim配置


# 介绍一下我的neovim配置

## 附上Pluglist

```c++
call plug#begin('~/.config/nvim/vim/plugged')
"美化插件
Plug 'hardcoreplayers/spaceline.vim'
" Plug 'itchyny/lightline.vim'
" Plug 'vim-airline/vim-airline'
" Plug 'vim-airline/vim-airline-themes'

" Plug 'liuchengxu/eleline.vim'
Plug 'bagrat/vim-buffet'
Plug 'luochen1990/rainbow'
Plug 'kristijanhusak/vim-hybrid-material'
Plug 'hardcoreplayers/oceanic-material'
Plug 'mhartington/oceanic-next'
Plug 'hardcoreplayers/dashboard-nvim'
Plug 'morhetz/gruvbox'
" Plug 'octol/vim-cpp-enhanced-highlight',{'for':'cpp'} " c++高亮
Plug 'Yggdroot/indentLine'                            " 缩进可视化
Plug 'ryanoasis/vim-devicons'                         " 给各种插件增加文件图标
Plug 'chrisbra/changesPlugin'                         " 文件修改提示
Plug 'itchyny/vim-cursorword'                         " 光标在单词上会有一个下划线
Plug 'kristijanhusak/defx-icons'
"功能插件 :使用更顺畅
Plug 'chxuan/vim-edit'
Plug 'gcmt/wildfire.vim'                                                                  " 智能选中enter
Plug 'suan/vim-instant-markdown',  {'for': 'markdown'}                                    " markdown预览
Plug 'dhruvasagar/vim-table-mode', {'on':'TableModeToggle'}                               " 更规范的表格
Plug 'kshenoy/vim-signature'                                                              " 书签跳转，ma
Plug 'junegunn/vim-easy-align'                                                            " 快速对齐 ,a2<space>第二个空格对齐，,a-<space>倒数，,a*<space>所有，,a<Enter>*<space>右对齐
Plug 'easymotion/vim-easymotion',  {'on':['<Plug>(easymotion-w)','<Plug>(easymotion-b)']} " 快速移动
Plug 'terryma/vim-smooth-scroll'                                                          " 平滑翻页
Plug 'rhysd/clever-f.vim'                                                                 " 智能F，搜索高亮，f跳转
Plug 'rhysd/accelerated-jk'                                                               " 加速jk键
Plug 'tpope/vim-repeat'                                                                   " 增强．功能，可以重复surround
Plug 'junegunn/vim-slash'                                                                 " 搜索后移动取消高亮
Plug 'itchyny/screensaver.vim',    {'on': 'ScreenSaver'}                                  " 屏幕保护程序
Plug 'jiangmiao/auto-pairs'                                                               " 自动补全括号
Plug 'tpope/vim-commentary'                                                               " 注释插件
Plug 'tpope/vim-surround'                                                                 " yss"加＂号，csw'" ＇修改成＂　ds'删除＇
" Plug 'vim-scripts/fcitx.vim',      {'for': ['markdown','cpp','vim','sh']}                 " 切换中文不影响普通模式输入
" Plug 'vim-scripts/VimIM'
Plug 'ZSaberLv0/ZFVimIM'
Plug 'ZSaberLv0/ZFVimJob'
Plug 'ZSaberLv0/ZFVimGitUtil' " 可选, 如果你希望定期自动清理词库 push 历史
Plug 'YourUserName/ZFVimIM_pinyin_base' " 你的词库
Plug 'ZSaberLv0/ZFVimIM_openapi' " 可选, 百度云输入法
" 功能插件:
Plug 'dense-analysis/ale'                                                                                    " 错误提示
Plug 'neoclide/coc.nvim',            {'branch': 'release'}                                                   " 自动补全
Plug 'honza/vim-snippets'                                                                                    " 代码片
Plug 'yianwillis/vimcdoc'                                                                                    " vim中文手册
Plug 'mbbill/undotree',              {'on':'UndotreeToggle'}                                                 " 撤销树（代码回滚）
Plug 'junegunn/fzf',                 {'on':['Files', 'History', 'Colors', 'Rg', 'Marks'] }                   " fzf模糊查找文件
Plug 'junegunn/fzf.vim',             {'on':['Files', 'History', 'Colors', 'Rg', 'Marks']}
Plug 'sbdchd/neoformat',             {'on':'Neoformat'}                                                      " 格式化文件(我还没用过)leader>nf
Plug 'voldikss/vim-floaterm',        { 'on': 'FloatermNew' }                                                 " 浮动终端
Plug 'liuchengxu/vista.vim',         {'on':'Vista'}                                                          " 查看函数什么的
Plug 'kristijanhusak/defx-git',      {'on':'Defx'}                                                           " 查看文件树
Plug 'Shougo/defx.nvim',             { 'do': ':UpdateRemotePlugins'}
Plug 'tyru/open-browser.vim',        {'on':['<Plug>(openbrowser-smart-search)', '<Plug>(openbrowser-open)']} " gx google搜索, gu打开连接
Plug 'mg979/vim-visual-multi',       {'branch': 'master'}                                                    " <c-n> 多鼠标操作
Plug 'voldikss/vim-translator',      { 'on':'<Plug>Translate' }                                              " 划词翻译 leader>tl
Plug 'junegunn/goyo.vim',            {'on':'Goyo'}                                                           " 专注模式gy开启
Plug 'tweekmonster/startuptime.vim', {'on': 'StartupTime'}                                                   " 查看启动所需时间
" 可选
"Plug 'sheerun/vim-polyglot',{'for':['c', 'h', 'cpp', 'py', 'go', 'java', 'vim', 'json', 'hs']}
"Plug 'vim-scripts/vim-auto-save'
"Plug 'kien/rainbow_parentheses.vim'
"Plug 'Yggdroot/LeaderF', { 'do': './install.sh' } " 文件搜索
"Plug 'wakatime/vim-wakatime'                      " 统计代码时间
"Plug 'SirVer/ultisnips'
"Plug 'rhysd/github-complete.vim'
"Plug 'simnalamburt/vim-mundo'                     "  撤销树可视化


call plug#end()
```

## StartupTime

> Total Time:  120.288 -- Flawless Victory
>
> Slowest 10 plugins (out of 33)~
>        [runtime]	35.025  
>          [vimrc]	28.422  
>         coc.nvim	10.588  
>       vim-buffet	10.202  
> vim-visual-multi	5.184   
>         ZFVimJob	4.578   
>          ZFVimIM	4.135   
>     vim-devicons	3.060   
>    vim-signature	2.727   
>              ale	2.355   

我的nvim配置地址：https://github.com/peapio/nvim


