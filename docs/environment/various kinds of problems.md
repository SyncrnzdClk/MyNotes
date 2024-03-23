# problems and solving
这部分内容主要是因为每天都被配置环境折磨，所以尽量留下一些痕迹和经验。

## mkdocs
曾经我下载完anaconda之后为了图方便，把他加到了环境变量中，结果后来anaconda没成功弄好，但是把机器上其他程序的默认python解释器的路径都改掉了，比如mkdocs。

然后我直接使用了`python -m mkdocs ...`来进行相关操作，发现可以了，原因是我原来的python还是正常的。

## anaconda/jupyter notebook
接上文，在我的机器上尝试使用anaconda出错之后，我就使用了wsl来尝试，发现大部分过程还是能成功，但是最后开启jupyter notebook的时候却没有找到设置的虚拟环境中的包。

最后我直接用了vscode，下载了jupyter notebook 和 python extensions的插件，发现在vscode里面还是能找到相应的虚拟环境的，而且vscode用起来也比直接用jupyter notebook舒服多了。