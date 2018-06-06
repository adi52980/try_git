func main() {
	bot, err := linebot.New(
		os.Getenv("962ef71b2efa6b9c4f6e98e8eefea517"),
		os.Getenv("w3/Rd3AHKq/GSxuGnf1XmUoRSiwp27mHnH3hr2PULtBhuY7XzpK0zC/8FpYMrdPGJQRrGH46PYVkj1dYTG5JfESX+IPF31ent3A0k9TI75F+GZkDsXQxw8YHlx5LKEZ8lCklh6aCCVisPA+iHDToFQdB04t89/1O/w1cDnyilFU="),
	)
	if err != nil {
		log.Fatal(err)
	}

	// Setup HTTP Server for receiving requests from LINE platform
	http.HandleFunc("/callback", func(w http.ResponseWriter, req *http.Request) {
		events, err := bot.ParseRequest(req)
		if err != nil {
			if err == linebot.ErrInvalidSignature {
				w.WriteHeader(400)
			} else {
				w.WriteHeader(500)
			}
			return
		}
		for _, event := range events {
			if event.Type == linebot.EventTypeMessage {
				switch message := event.Message.(type) {
				case *linebot.TextMessage:
					if _, err = bot.ReplyMessage(event.ReplyToken, linebot.NewTextMessage(message.Text)).Do(); err != nil {
						log.Print(err)
					}
				}
			}
		}
	})
	// This is just sample code.
	// For actual use, you must support HTTPS by using `ListenAndServeTLS`, a reverse proxy or something else.
	if err := http.ListenAndServe(":"+os.Getenv("PORT"), nil); err != nil {
		log.Fatal(err)
	}
}
