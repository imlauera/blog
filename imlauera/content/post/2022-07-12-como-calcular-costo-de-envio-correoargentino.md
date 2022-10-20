---
layout: post
title: Calcular costo de envio CorreoArgentino
date: 2022-07-12 09:08 -0300
---

Es increíble que el servicio de paqueteria ecommerse (paq.ar) de CorreoArgentino todavia no haya desarrollado una API para calcular el costo de envío a diferentes partes del país, en lugar de una API te dan un PDF en donde se muestran dos tablas; una tabla tiene los diferentes pesos del producto, las zonas y sus respetivos precios y la otra con el país de origen y de destino y las diferentes zonas correspondientes.

<a href="/assets/files/lista-de-precios-CF-MiCorreo.pdf">PDF de Costos (Copia Local)</a><br/>

<a href="https://www.correoargentino.com.ar/MiCorreo/public/files/lista-de-precios-CF-MiCorreo.pdf">https://www.correoargentino.com.ar/MiCorreo/public/files/lista-de-precios-CF-MiCorreo.pdf (Link Externo)</a>


Y con esa informacion ya deberias arreglarte para poder calcular el costo del envio aunque ellos te aclaran que los precios pueden sufrir modificaciones sin previo aviso xd quizas se pueda parsear el PDF y usar algun tipo de expresion regular para obtener los precios de las diferentes zonas sin tener que hacerlo manualmente.
