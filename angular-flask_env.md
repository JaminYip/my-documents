#AngularとFlask環境構築

Node.jsインストール  
※公式サイトから

https://nodejs.org/ja/

|コマンド|バージョン|備考|
|----|----|----|
|node --version|v12.14.1|installed at 2020 1/11|
|npm --version|6.13.4|〃|

①コマンド「[sudo] npm install -g angular-cli」を実行する

⚠️以下のエラーが発生した場合
````
npm WARN checkPermissions Missing write access to /usr/local/lib/node_modules
npm ERR! code EACCES
npm ERR! syscall access
npm ERR! path /usr/local/lib/node_modules
npm ERR! errno -13
npm ERR! Error: EACCES: permission denied, access '/usr/local/lib/node_modules'
npm ERR!  [Error: EACCES: permission denied, access '/usr/local/lib/node_modules'] {
npm ERR!   stack: "Error: EACCES: permission denied, access '/usr/local/lib/node_modules'",
npm ERR!   errno: -13,
npm ERR!   code: 'EACCES',
npm ERR!   syscall: 'access',
npm ERR!   path: '/usr/local/lib/node_modules'
npm ERR! }
npm ERR! 
npm ERR! The operation was rejected by your operating system.
npm ERR! It is likely you do not have the permissions to access this file as the current user
npm ERR! 
npm ERR! If you believe this might be a permissions issue, please double-check the
npm ERR! permissions of the file and its containing directories, or try running
npm ERR! the command again as root/Administrator.

npm ERR! A complete log of this run can be found in:
npm ERR!     /Users/********/.npm/_logs/2020-01-11T10_39_14_992Z-debug.log
````

以下のコマンドを実行する(npmのデフォルトディレクトリを作成する)
````
mkdir ~/.npm-global
npm config set prefix '~/.npm-global'
echo ' export PATH=~/.npm-global/bin:$PATH' >> ~/.bash_profile
source ~/.bash_profile
````

②コマンド「ng new [プロジェクト名]」を実行する

⚠️ngがインストールされていて、「bash: ng: command not found」が出力された場合
````
コマンド「alias ng="/Users/********/.npm-global/lib/node_modules/@angular/cli/bin/ng"」を実行する  
※ng="〜"はインストールした場所によって変わるため、適宜変更する。  
「npm install -g angular/cli」を実行時にインストール場所がターミナルに表示されているはずなので、それを入力する。
````

③pythonファイルを作成

app.py
````
from flask import Flask, render_template

app = Flask(__name__)


@app.route('/')
def hello():
    return render_template('index.html')


app.run()
````

④コマンド「ng build --base-href /static/」を実行する
