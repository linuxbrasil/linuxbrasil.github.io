---
layout: post
title: "Howto de instalação do Arch Linux"
description: "Guia de instalação do Arch Linux"
date:   2020-05-17 22:45:00 -0300 
categories: ArchLinux
by: 'Reginaldo'
telegram: '@Saitam10'
icon: 'settings' 
questions:
  - question: 'Howto de instalação do Arch Linux'
    answer: '
    <p>Download da imagem ISO: <a href="magnet:?xt=urn:btih:f95c371d5609d15f6615139be84edbb5b94a79bc&dn=archlinux-2020.05.01-x86_64.iso&tr=udp://tracker.archlinux.org:6969&tr=http://tracker.archlinux.org:6969/announce" target="_blank"> magnet ISO ArchLinux </a> </p>

    <b>Verificar a assinatura da imagem ISO</b>

    <code>
    $ gpg --keyserver-options auto-key-retrieve --verify archlinux-versão-x86_64.iso.sig
    </code>

    <p>OU a partir de uma instalação existente</p>

    <code>
    $ pacman-key -v archlinux-versão-x86_64.iso.sig
    </code>

    <p>Após gravar a imagem ISO do Arch Linux, inicialize o ambiente</p>

    <p>Quando o menu do Arch aparecer, selecione Boot Arch Linux e pressione Enter para entrar no ambiente de instalação</p>

    <b>Definir o layout do teclado</b>

    <p>Exibir o mapa de teclado</p>
    <code>
    # ls /usr/share/kbd/keymaps/**/*.map.gz
    </code>

    <p>Se o teclado for ABNT2</p>

    <code>
    # loadkeys br-abnt2  
    </code>

    <p>Case o teclado for de português de Portugal</p>

    <code>
    # loadkeys pt-latin1 
    </code>

    <b>Definir o idioma do ambiente</b>

    <p>O ambiente live vem em inglês (locale en_US.UTF-8) por padrão, mas você pode alterá-lo para executar as etapas de instalação usando o idioma desejado.</p>

    <p>Para português brasileiro, descomente pt_BR.UTF-8 UTF-8 e qualquer outro locale desejado em /etc/locale.gen e gere-os com:</p>

    <code>
    # locale-gen
    </code>

    <p>Então, exporte a variável LANG acrescentando o idioma e codificação desejados. Por exemplo, para português brasileiro seria:</p>

    <code>
    # export LANG=pt_BR.UTF-8
    </code>

    <p>Para português de Portugal, use pt_PT.UTF-8 UTF-8 em vez do "pt_BR".</p>

    <b>Atualizar o relógio do sistema</b>

    <code>
    # timedatectl set-ntp true
    </code>

    <b>Particionamento do disco rígido</b>

    <p>Exibe o dispositivo do disco rígido com o comando</p>

    <code>
    # fdisk -l
    </code>

    <p>Resultados terminando em rom, loop ou airoot podem ser ignorados.</p>

    <p>Se for instalação apenas Linux no computador, então precisará criar uma partição EFI, se for UEFI</p>

    <code>
    # cfdisk /dev/sda 
    </code>

    <pre>
    /boot/efi de 100MB
    / de 20GB
    /home restante do espaço
    </pre>

    <b>Formatação das partições criadas</b>

    <code>
    # mkfs.ext4 /dev/sda1 (/boot/efi)
    <code>

    <code>
    # mkfs.ext4 /dev/sda2 (/)
    </code>

    <code>
    # mkfs.ext4 /dev/sda3 (/home)
    <code>

    <b>Montar o sistema de arquivo</b>

    <code>
    # mount /dev/sda1 /boot/efi
    </code>

    <code>
    # mount /dev/sda2 /
    </code>

    <code>
    # mount /dev/sda3 /home
    </code>

    <b>Instalação de pacotes essenciais</b>

    <code>
    # pacstrap /mnt base linux linux-firmware
    </code>

    <b>Configurar o sistema</b>

    <code>
    # genfstab -U / >> /etc/fstab
    </code>

    <b>Chroot</b>

    <code>
    # arch-chroot /
    </code>

    <b>Fuso horário</b>

    <code>
    # ln -sf /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime
    </code>

    <code>
    # hwclock --systohc
    </code>

    <b>Localização</b>

    <p>Edite /etc/locale.gen e descomente pt_BR.UTF-8 UTF-8 com qualquer outro locale necessário. Gere os locales executando:</p>

    <code>
    # locale-gen
    </code>

    <p>Crie o arquivo locale.conf e defina a variável LANG adequadamente:</code>
    <pre>
    /etc/locale.conf
    LANG=pt_BR.UTF-8
    </pre>

    <p>Se você definir o layout do teclado, torne as alterações persistentes em vconsole.conf:</p>
    <pre>
    /etc/vconsole.conf
    KEYMAP=br-abnt2
    </pre>

    <b>Crie o arquivo hostname:</b>

    <code>
    # vim /etc/hostname
    </code>
    <pre>
    Saitam
    </pre>

    <p>Adicione entradas correspondentes ao hosts</p>

    <code>
    # vim /etc/hosts
    </code>

    <pre>
    127.0.0.1	localhost.localdomain	localhost
    ::1		localhost.localdomain	localhost
    127.0.1.1	meuhostname.localdomain	Saitam
    </pre>


    <b>Initramfs</b>

    <p>Criar um novo initramfs geralmente não é necessário, porque mkinitcpio foi executado na instalação do pacote de kernel com pacstrap.</p>

    <code>
    # mkinitcpio -P
    </code>

    <b>Password do root</b>

    <code>
    # passwd
    </code>

    <b>Gerenciador de boot</b>

    <p>Nesse howto foi usado o GRUB</p>

    <code>
    # grub-install --target=x86_64-efi --efi-directory=esp --bootloader-id=GRUB
    </code>

    <b>Reincie</b>

    <p>Saia de ambiente chroot digitando exit ou pressionando Ctrl+D. </p>   

    <b>Referência:</b>

    <a href="https://wiki.archlinux.org/index.php/Installation_guide" target="_blank"> Wiki instalação do ArchLinux </a>
    '
        image: "posts/archlinux-install.png"


---