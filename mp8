#!/bin/bash

pasue(){
    echo $*
    read -s -n1 -p "press any key to continue.."
    echo
}

check(){
    info=`./gold $1 ./gold.png $2 2>&1`
    if [[ "$info" =~ "Image too large" ]]; then return; fi
    if [[ "$info" =~ "must lie within" ]]; then return; fi

    ./mp8 $1 ./output.png $2 > /dev/null
    if [ $? != 0 ]
    then
        echo ERROR: Runtime Error
        pasue $1 $2
    fi
    ./gold $1 ./gold.png $2 > /dev/null
    cmp ./output.png ./gold.png > /dev/null
    if [ $? != 0 ]
    then
        echo ERROR: Different Output
        pasue $1 $2
    fi
    echo Test Passed!
}

clear
make > /dev/null
if [ $? != 0 ]
then
    echo Compile Error!
    echo Exiting...
    exit
fi
for img in Images/*
do
    for option in 1 2 3
    do
        for xy in "30 30" "45 50" "80 60" "350 120" "500 220"
        do
            argu="$option $xy 3388FF"
            if [ $option != 1 ]
            then
                for distSq in 10 50 160 400 1400
                do
                    check "$img" "$argu $distSq"
                done
            else
                check "$img" "$argu"
            fi 
        done
    done
done

