### Shell scripting

Loop over files in a directory & convert via LAME

    for i in *.wav ; do
    echo $i
    b=`basename "$i" .wav`
    echo $b
    lame -V0 "$i" "$b.mp3"
    done

---*

#### Environment Variables
Show current environment variables loaded in session

    printenv

Add a temporary environment variable to current session

    export ENV_VAR_NAME='some_string'

Add a environment variable to load in all sessions. There are multiple ways. There are multiple ways. First check `/etc/paths` to see the load order. After that check the following files:

    .profile
    .bashrc (Linux)
    .bash_profile (Mac)
