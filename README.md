# Solution1
C#ソースコードをGitHubで管理してみる。


# GitHub に新しいリポジトリを作成して、これから新規作成するC#のソースコードを管理できる状態にする手順。


# 環境
	[Signup]アカウント登録      https://github.com/

	macOS Ventura
	zsh                     既定のShell
	.NET 7.0                https://learn.microsoft.com/ja-jp/dotnet/core/install/macos
	Visual Studio Code      https://code.visualstudio.com/
	Homebrew                https://brew.sh/index_ja    （メモ 一時的に bash に切り替えてインストール。）
	GitHub CLI              https://cli.github.com/
	micro                   https://micro-editor.github.io/    （メモ ~/.zprofile に、export EDITOR=micro を記述。）


# GitHub CLI を利用してGit Hubを操作できるようにするための準備をする。

	1. 個人用アクセストークンを作成する。

		参考ドキュメント
		「fine-grained personal access token の作成」
		https://docs.github.com/ja/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token

		<ブラウザ>

		あなたのアカウント管理ページより
		https://github.com/

		Settings > Developer settings > Psersonal access tokens > Fine-grained tokens > Generate new token
		
		>>> ここで作成されたトークンは
		>>> 次の How would you like to authenticate GitHub CLI?にて、[Paste an authentication token] を選択した場合に内容をコピーしておく必要があるが、
		>>> [Login with a web browser]ならコピーする必要はない。


	2. GitHubへのログイン認証。コマンドを入力後、アシスタントに従って順に進める。

		<ターミナル>

		# pwd
		# /Users/xxxxxx

		gh auth login

		アシスタント
			? What account do you want to log into [GitHub.com]
			? What is your preferred protocol for Git operations [HTTPS]
			? Authenticate Git with your GitHub credentials? [Yes]
			? How would you like to authenticate GitHub CLI?

				[Login with a web browser]（こちらを推奨）
				を選択した時は、
					! First copy your one-time code: ＊＊＊＊-＊＊＊＊
					Press Enter to open github.com in your browser...

					{Enter}キーを押すと、ブラウザが起動。
					ワンタイムコードを催促されるので、＊＊＊＊-＊＊＊＊に表示されている値を入力する。

				[Paste an authentication token]
				 を選択した時は、
					「1. fine-grained personal access token」のトークンを貼り付ける。


# ”Solution1”という名前の公開リポジトリをGitHub上に作成する。その複製（クローン）をローカルに作成する。

	1. ローカルの作業場所として、ワークツリーのルート（トップ）を作成する。

		<ターミナル>

		# pwd
		# /Users/xxxxxx

		mkdir github

		cd github

	2. ”Solution1”という名前のリポジトリを新規作成する。

		<ターミナル>

		# pwd
		# /Users/xxxxxx/github
		#
		# ls -a
		# .    ..

		gh repo create

		アシスタントに従って設定をする。
			? What would you like to do? [Create a new repository on GitHub from scratch]
			? Repository name [Solution1]
			? Description [何でもいいから説明を書く]
			? Visibility [Public]
			? Would you like to add a README file? [Yes]
			? Would you like to add a .gitignore? [Yes]
			? Choose a .gitignore template [C++]（作り直すのでどれを選んでも良い）
			? Would you like to add a license? [Yes]
			? Choose a license [MIT License]
			? This will create "Solution1" as a public repository on GitHub. Continue? [Yes]
			? Clone the new repository locally? [Yes]

		# ls -a
		# .    ..    Solution1


# ソース管理から除外するファイルのリストを作成する。

	1. C＃ソースを管理するにあたり、一般的に除外すべきファイルの一覧を、生成してもらう。

		<ブラウザ>

		https://www.toptal.com/developers/gitignore

		[macOS] [VisualStudioCode] [Csharp]　を入力して、[作成する]ボタンを押す。

		表示された内容を全て選択して、コピーする。

	2. .gitignoreファイルの内容を、全て置き換える。

		<ターミナル>

		cd Solution1 

		# pwd
		# /Users/xxxxxx/github/Solution1
		#
		# ls -a
		# .    ..    .git    .gitignore    LICENSE    README.md

		pbpaste > .gitignore


# Csharpコンソールアプリを作成する。

	<ターミナル>

	# pwd
	# /Users/xxxxxx/github/Solution1

	dotnet new sln

	dotnet new console --name ConsoleApp1 --output ./ConsoleApp1/

	dotnet sln add ConsoleApp1/ConsoleApp1.csproj

	# cat ConsoleApp1/Program.cs 
	# Console.WriteLine("Hello, World!");

	dotnet run --project ConsoleApp1
	# Hello, World!

	dotnet publish


# 作成したソースコードをGitHubに登録（変更を適用）する。

	<ターミナル>

	# pwd
	# /Users/xxxxxx/github/Solution1

	1. （ローカル）ワークツリーから、インデックスに登録する。

		<ターミナル>

		git add .

	2. （ローカル）インデックスから、リポジトリに登録する。コメントを必ず書くこと。

		<ターミナル>

		git commit

		>>> vim が起動してしまった時は、[ESC]を押して、:q!を入力して{Enter}キーを押す。

		>>> vimに不慣れなので、スクリーンエディタをmicroに変更している。
		>>> ctrl+[Q]キーが、VSCodeと衝突してしまうので、ctrl+[E]の後 quit と入力して終了する。

	３. （ローカル）リポジトリから、（リモート）公開している”Solution1”リポジトリへ変更を適用する。

		<ターミナル>

		git push




