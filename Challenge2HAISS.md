# WidgetApp's Streaming API Article (Draft)

Developed by Anonymous Ltd., **WidgetApp** is a web-based software system that lets 
you design Things. This article will cover what I've learned from the Engineering team 
about their new Streaming API.

## Overview 

Streaming APIs are used to examine data in real-time for users to gather up-to-date
information and accurate results through the web. 
With this new Streaming API, users can scroll through the homepage of **WidgetApp** and 
then select a Thing to design. Once selected, they can start working on it using the 
editor. 

Most actions of the editor work by calling AJAX (Asynchronous JavaScript and XML)
endpoints, allowing updates without having to reload the web page. 

## Streaming frontend (SFE)

Because this API is streaming over WebSocket, exposing real-time data, multiple users
can simultaneously work on the same Thing design. It's important that any changes made are 
quickly communicated so that they can be seen by all clients. 

## Connection details

In order to communicate using WebSocket, you'll need to create a `WebSocket` object which
will attempt to open the connection to the server. 
Authentication is done over a secure WSS protocol and the URL to which to connect is 
`www.widgetapp.com/_stream`. 
For example, `wws://www.widgetapp.com/_stream`.

The initial request made by the API goes to [Cloudflare](https://www.cloudflare.com/),
then routed to the Streaming frontend. 

### Multiple services on one WebSocket connection

Different services can use the same WebSocket connection. How this works is, the
Streaming frontend:

1. Accepts the connection at the server.
2. Using its filter chain, builds the request context.
3. Splits the stream by the service.
4. Connects them to the corresponding services. 

# How I approached creating this article

Firstly, for this article, I thought about the order of content that the reader would be 
able to learn more about the new Streaming API. I believe an overview, describing why or 
how it's used is important to start out with. I did some research on Streaming APIs and 
how WebSocket works in order to effectively communicate details about connection. For 
this article, I'm assuming that building a WebSocket API from scratch is not necessary,
and that describing how this is done is already known by the audience being familiar with 
WidgetApp's other APIs.

## Questions and missing details to complete this article

1. It would be helpful to show an example of or available AJAX endpoints. Since users are
   first interacting with the editor, perhaps available editor actions would be useful.
2. Should there be more details on authentication?
3. What format can responses be in? Should examples be provided? 