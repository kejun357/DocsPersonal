##### 舍弃本地修改
- 未使用 git add 缓存代码时： git checkout .
- 已使用 git add 缓存代码时： git reset HEAD .
- 已使用 git commit 提交代码时：git reset --hard HEAD^ 回退到上一次commit状态。 git reset --hard coomitid 回退到任何版本 (git log 查看提交历史)


# rebase
` 不要在公共分支使用rebase `
- 1-2-3 是现在的分支状态
- 这个时候从原来的master ,checkout出来一个prod分支
- 然后master提交了4.5，prod提交了6.7
- 这个时候master分支状态就是1-2-3-4-5，prod状态变成1-2-3-6-7
- 如果在prod上用rebase master ,prod分支状态就成了1-2-3-4-5-6-7
- 如果是merge
    1-2-3-6-7-8
    ........ |4-5|
    会出来一个8，这个8的提交就是把4-5合进来的提交

##### merge和rebase实际上只是用的场景不一样
    更通俗的解释一波.
    比如rebase,你自己开发分支一直在做,然后某一天，你想把主线的修改合到你的分支上,做一次集成,这种情况就用rebase比较好.把你的提交都放在主线修改的头上
    如果用merge，脑袋上顶着一笔merge的8,你如果想回退你分支上的某个提交就很麻烦,还有一个重要的问题,rebase的话,本来我的分支是从3拉出来的,rebase完了之后,就不知道我当时是从哪儿拉出来的我的开发分支
    同样的,如果你在主分支上用rebase, rebase其他分支的修改,是不是要是别人想看主分支上有什么历史,他看到的就不是完整的历史课,这个历史已经被你篡改了

#### rebase 常用指令
- git rebase -i dev 可以将dev分支合并到当前分支

` 本地和远端对应同一条分支,优先使用rebase,而不是merge `



