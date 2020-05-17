---
layout: post
title: "Git deploy na VPS"
description: "A idéia desse artigo é mostrar como configurar um deploy automatizado"
date:   2020-05-16 22:30:00 -0300
categories: vps
by: 'Reginaldo'
telegram: 'saitam10'
icon: 'activity'
questions:
  - question: 'Git deploy na VPS'
    answer: '
		<p>Considerando que já tenha configurado o ambiente e esteja funcionando na VPS, incluindo o GIT. Chegou a hora de automatizar o deploy da aplicação. Esse é o objetivo deste post.</p>

		<p>Na VPS cria dois diretórios, uma para o repositório e outro para aplicação</p>

		<p>repositório: <b>/var/repo/projeto.git</b></p>
		<p>aplicação: <b>/var/www/html/projeto</b></p>

		<code>
		# mkdir /var/repo<br>
		# mkdir /var/repo/projeto.git<br>
		# cd /var/repo/projeto.git<br>
		# git init --bare<br>
		# cd hooks<br>
		# vim post-receive
		</code>

		<code>
		#!/bin/bash<br>
		git --work-tree=/var/www/html/projeto --git-dir=/var/repo/projeto.git checkout -f
		</code>

		<p>ESC +:wq (Salvar e sair do editor Vim)</p>

		<code>
		# chmod +x post-receive<br>
		# chown -R usuario:usuario /var/repo/projeto.git<br>
		<br>
		# mkdir /var/www/html/projeto<br>
		# chown  R www-data:www-data /var/www/html/projeto
		</code>

		<p>Agora na máquina de desenvolvimento</p>
		<p>Acesse o diretório do projeto, execute</p>
		<p>Adicionar o repositório deploy da VPS no remote</p>

		<code>
		git remote add deploy ssh://usuario@IP_VPS/var/repo/projeto.git<br>
		git add .<br>
		git commit -m "primeiro commit"<br>
		git push origin master<br>
		git push deploy master
		</code>
		
		<p>Para visualizar os commits</p>
		
		<code>
		git log --all --graph --decorate --oneline
		</code>

		<p>Caso ocorra algum erro de permissão, execute o hooks/post-receive manualmente</p>

		<code>
		#cd /var/repo/projeto.git/hooks<br>
		#./post-receive
		</code>

		Feito!'
    image: "posts/vps.jpg"
---
