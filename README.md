# shh
(not)secret shell goodies

## date_to_rfc2822
portable-ish way to convert any date format into a valid RFC2822 date:

	# convert input date to RFC2822
	# $1 - input date
	# $2 - input date format; see strftime(3)
	date_to_rfc2822() {
		date="$1"
		format="$2"
		rfc2822="+%a, %d %b %Y %T %z"

		# if on Linux, use GNU date syntax
		if [ "$(uname)" = "Linux" ]; then
			date -d "$date" "$rfc2822"
		else
			date -j -f "$format" "$date" "$rfc2822"
		fi
	}

example usage:

	$ date_to_rfc2822 '2021-01-30 12:13' '%F %I:%M
	Sat, 30 Jan 2021 12:13:02 +1000
