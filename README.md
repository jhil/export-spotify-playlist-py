## export-spotify-playlist.py
Quick and dirty python script 
for exporting Spotify playlist
with album date information
in CSV format.

## Installation
Requires spotipy https://github.com/plamere/spotipy

`pip install spotipy`

Note that spotipy requires the Requests library,
pip should take care of that though.

## Usage
Get a Spotify client id and client secret
by registering an app (this app really)
at https://developer.spotify.com/my-applications/.
Set its redirect url to 'http://localhost' (when registering).

Set the following environment variables:
    SPOTIPY_CLIENT_ID=<your-client-id>
    SPOTIPY_CLIENT_SECRET=<your-client-secret>
    SPOTIPY_REDIRECT_URI='http://localhost'`

For example do this in the terminal where you want to run the script
(in Linux, do something similar on Windows):
    export SPOTIPY_CLIENT_ID=<your-client-id>
    export SPOTIPY_CLIENT_SECRET=<your-client-secret>
    export SPOTIPY_REDIRECT_URI=http://localhost

Finally run the script as:
`python export-spotify-playlist.py PLAYLISTURI > playlist.csv`

PLAYLISTURI's can be found in the Spotify app 
by right-clicking a playlist and selecting "Copy Spotify URI". 
It has a format like `spotify:user:<username>:playlist:<some-id>`
 
The script prints a message to stderr
for each batch of tracks it processes.
Redirecting output to file with `> playlist.csv`
will not redirect this message
so your .csv file will not contain these messages.

Spotipy will open a web browser (or new tab)
for authentication with Spotify 
if it is the first time you use the script.
When you login you'll be redirected to `localhost/?code=<long-id>`



which will very likely result in some unable-to-connect error in your browser.
Don't worry, you only need the actual url (`localhost/?cod=<long-id>`).
Copy it and paste it back into the terminal where the python script is running.
The script also instructs you to do so.

## TODO / Notes
### CSV format:
Right now it just exports unquoted data separated by semicolon (;).
So if your track title or album title contains a semicolon
you'll have surprises when parsing the output. 

Find a better solution or change the separator based on your needs.

### Deleting login token:
There is a hidden dir `.cache-<username>` which store
the login token from run to run. 
If nothing seems to work try deleting this and reauthenticating,
e.g. after you changed password of your Spotify account.
