### Shell scripting

Loop over files in a directory & convert via LAME

    for i in *.wav ; do
    echo $i
    b=`basename "$i" .wav`
    echo $b
    lame -V0 "$i" "$b.mp3"
    done
