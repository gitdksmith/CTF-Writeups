# Networks 200 - Obfuscated Javascript

1. Prompt: "We heard a rumour that our website will be used to distribute malware. We believe we captured a test run of it. Can you find out what the malicious content will be?", with link to malwaretestrun.tgz.

2. Opening the gziped tar we get malware-testrun.pcap.

3. Opening the pcap with wireshark we see http traffic requesting webpages and a lot of images. Extract all http elements to a new directory.

4. Reconstruct the site correctly by making an 'images' direcotory and moving all images to it, except for notit.png.

5. The root html page is saved as %2f, not sure if you can open it in firefox so I just moved it to index.html

6. Run 'firefox index.html' and enjoy the obama memes and advertisement. Don't worry, there is no real malware.

7. Look into ads.html where you will see base64 encoded data in an image tag, which will be run through eval().

8. Run it through a decoder/beautifier and see that data is being extracted from notit.txt.

9. You can modify ads.html to include this code directly, like in [adsShowHiddenJS.html](adsShowHiddenJS.html), intead of having to make modifications to it, base64 encoding it, copying it in, etc.

10. To see what would be run through eval in function a, use console.log to output to the console view in firefox.

11. Change notit.png to ad001.png, ad002.png, etc. and run firefox for each one. You will see that the output of each is a string like "[])[+!+[]]]((!![]+[])". This is javascript using hieroglyphy encoding: https://stackoverflow.com/questions/25622221/language-made-only-of-brackets-plus-and-exclamation-marks

12. Concatinate all outputs and run it through the javascript console to get the flag.

**Flag:**
"x=new Date();if(x.getDate()=="23"&&x.getHours()=="12"){alert("flag{02aa1488771e325eef9b0e5f0d2db626}")}"
