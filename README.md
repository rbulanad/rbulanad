VIMRC
:set showcmd
:set tabstop=4
:set shiftwidth=4
:set smartindent
:set mouse=a
:set nu
function! MultiReplace(...)
	let pairs = len(a:000)
	if pairs % 2 != 0
		echo "Invalid num of args"
		return
	endif
	for i in range(0, pairs - 1, 2)
		let old = a:000[i]
		let new = a:000[i + 1]
		execute '%s/' . old . '/' . new . '/gc'
	endfor
endfunction

command -nargs=* SS call MultiReplace(<f-args>)

nnoremap <silent> s ostd::cout << "" << std::endl;<ESC>14hi
nnoremap <silent> m iint	main()<CR>{<CR>return (0);<CR>}<ESC>

function! GetCNAME()
	let g:CNAME = input('Enter a class name: ')
	call PrintClass()
endfunction

function! PrintClass()
	if empty(g:CNAME)
		echom "Error: I need a name for the class"
	else
		execute 'normal! i#ifndef ' . toupper(g:CNAME) . "_HPP\<CR>#define " . toupper(g:CNAME) . "_HPP\<CR>\<CR>class	" . g:CNAME . "\<CR>" . "{\<CR>private:\<CR>public:\<CR>" . g:CNAME . "();\<CR>~" . g:CNAME . "();\<CR>" . g:CNAME . "(const " . g:CNAME . " &dup);\<CR>" . g:CNAME. " &operator=(const " . g:CNAME . " &dup);\<CR>};\<CR>\<CR>#endif\<ESC>"
	endif
endfunction

nnoremap <silent> c :call GetCNAME()<CR>

function! PrintClassDef(name)
	if empty(a:name)
		echom "Error: I need a name for the class"
	else
		execute 'normal! i#include "' . a:name . ".hpp\"\<CR>\<CR>" . a:name . "::" . a:name . "()\<CR>{\<CR>}\<CR>\<CR>" . a:name . "::~" . a:name . "()\<CR>{\<CR>}\<CR>\<CR>" . a:name . "::" . a:name . "(const " . a:name . " &dup)\<CR>{\<CR>*this = dup;\<CR>}\<CR>\<CR>" . a:name . " &" . a:name . "::operator=(const " . a:name . " &dup)\<CR>{\<CR>if (this != &dup) {}\<CR>return *this;\<CR>}\<CR>\<ESC>"
	endif
endfunction

command -nargs=1 CC call PrintClassDef(<q-args>)
