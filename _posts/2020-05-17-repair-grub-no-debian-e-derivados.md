---
layout: post
title: "Repair Grub no Debian e derivados"
description: "Comandos simlpes para facilitar a restauração."
date:   2020-05-17 17:25:00 -0300
categories: debian
by: 'Henry Jr'
icon: 'settings'
questions:
  - question: 'Repair Grub no Debian e derivados'
    answer: '<p>O uso &eacute; basicamente muito simples, use o terminal para os seguintes comandos.</p><p>Etapa 1. Inicialize seu USB na inicializa&ccedil;&atilde;o do sistema. Selecione a op&ccedil;&atilde;o &quot;live&quot;.</p><p>Etapa 2. Inicialize no Sistema Linux, abra o Terminal. Digite os seguintes comandos:</p><p><code>mount /dev/sda6 /mnt<br>for i in /dev /sys /run /proc; do mount --bind &quot;$i&quot; &quot;/mnt$i&quot;; done<br>chroot /mnt<br>grub-install /dev/sda<br>update-grub<br>exit</code></p><p>Etapa 3. Agora reinicie o sistema, voc&ecirc; ver&aacute; o menu de inicializa&ccedil;&atilde;o mostrando seu grub.</p><p>Na maioria das vezes, o Debian/Grub &eacute; reparado pelas etapas acima, mas, excepcionalmente, voc&ecirc; n&atilde;o pode, por isso &eacute; necess&aacute;rio executar mais comandos.</p><p>Etapa 4. Inicialize o Live novamente, abra o terminal digite os seguintes comandos:</p><p><code>apt-get install os-prober<br>os-prober<br>update-grub</code></p><p>Isso ajudar&aacute; muito a reparar o Grub.</p><p>Boa sorte!</p>'
    image: "posts/grub-rescue.png"
---
