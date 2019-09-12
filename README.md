# 《汇编语言（第2版）》郑晓薇

----

  ;9-3.asm  在屏幕的窗口中显示字符串并输入该字符串。
include 9-3.mac                    ;宏库
.model small
.data
letter db 'Every success in your study.',0ah,0dh,'$'
mess  db 29,32 dup(?)        
cont db ?
.code
start:
mov ax,@data            
mov ds,ax
clearsc                            ;清屏
clearsw                            ;开窗口
reptt:
;置显示光标
mov ah,2
mov dh,8                            ;在8行30列显示
mov dl,30
mov bh,0
int 10h
;显示串
mov ah,9
mov dx,offset letter
int 21h
;置输入光标
mov ah,2
mov dh,15                            ;在15行30列输入
mov dl,30
mov bh,0
int 10h
;输入串
mov al,0
mov ah,10
mov dx,offset mess
int 21h
;窗口内上卷
mov ah,6
mov al,1                            ;上卷1行
mov ch,8                            ;从8行30列到15行60列
mov cl,30
mov dh,15
mov dl,60
mov bh,27h                        ;绿底灰白字
int 10h
inc cont                            ;可输入3次
cmp cont,3
jne reptt
out1:
mov ah,4ch
int 21h
end start
宏库9-3.MAC: 
;9-3.mac BIOS宏库
;清屏clearsc
clearsc macro
mov ah,06h
mov al,0
mov bh,0F0h                            ;白底黑字
mov ch,0
mov cl,0
mov dh,23
mov dl,79
int 10h
mov dx,0                            ; 光标在屏幕左上角
mov ah,2
int 10h
endm
;开窗口                    
clearsw macro
mov ah,06h
mov al,0
mov bh,27h                            ;绿底灰白字
mov ch,8                            ;从8行30列到15行60列
mov cl,30
mov dh,15
mov dl,60
int 10h
endm
-----
