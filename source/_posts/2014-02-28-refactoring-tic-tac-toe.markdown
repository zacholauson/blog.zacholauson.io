---
layout: post
title: "Refactoring Tic Tac Toe"
date: 2014-02-28 08:34
categories: 

---

This week I mainly focused on refactoring my Tic Tac Toe for my next challenge which is to put my Tic Tac Toe on the web using the Clojure framework [Joodo](http://www.joodoweb.com/).

In Clojure there are Protocols which are a way of abstracting functions away from concretions, or a specific namespace.

This is how I had been determining whos player it was then asking for the next move depending on the player.

<script src="https://gist.github.com/zacholauson/35f6eeafb24df703afc4.js"></script>

This is bad because for one, it knows too much about something core or even tic tac toe itself shouldnt care about, and two, if I wanted to be able to play with 2 humans or 2 computers, this wouldnt work because its too coupled to a one computer one human game.

I then refactored the game to use a protocol for a Player and use a deftype Human and deftype Computer as my players and store them in a collection on my gamestate.

<script src="https://gist.github.com/zacholauson/7afc74783d274d905565.js"></script>

Having it set up like this is great because now, in my gamestate I have a collection with my players in it. Then when I need to get my next player, I can just grab the first player out of the collection and ask it for a move. It wont matter which players turn it is, it will just get the move because each player type has a different implementation for getting the next move.