1. the prompt points you too http://vod.stillhackinganyway.nl/
2. the page source has hint "<!-- Knock Knock 88 156 983 1287 8743 5622 9123 -->"
3. Its asking to be port knocked. Can do with netcat:
	nc -z vod.stillhackinganyway.nl 88 156 983 1287 8743 5622 9123;
-z is for scanning/no-io so there is no tcp resends that would mess  up the knock sequence
4. in the end you connect to 9123 and the response is the flag
flag{6283a3856ce4766d88c475668837184b}

