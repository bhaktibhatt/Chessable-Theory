### first regular chess game.
1. Understanding Javascript 
    - refer 2-game.html and 2-game.css for static design of the 2-player chess game. 
    - let's first see coloring function the below code snippet defines the function.
    1. coloring function
        ```
        function coloring() {
            const color = document.querySelectorAll('.box')
            color.forEach(color => {
                getId = color.id
                arr = Array.from(getId)
                arr.shift()
                aside = eval(arr.pop())
                aup = eval(arr.shift())
                a = aside + aup

                if (a % 2 == 0) {
                    color.style.backgroundColor = '#8F9EB8' //dark blueish white
                    }
                if (a % 2 !== 0) {
                    color.style.backgroundColor = '#C3CDDC' //light blueish white
                    }
            })
        }
        coloring()
        ```

        - The first line in definition body selects all the elements which has the class **".box"** and pass those values in a array *color*
        - Using the for each loop we iterate through all the elements of color 
        - in the loop we get the *id* of each element
        - next, convert this string form *id* into array elements stored in *arr* 
        - *arr.shift()* removes the 0th index element from the array;<br>- note: all ids are starting from letter b eg b102, b302 etc, here we need to work using math operation so we need a to convert this string into a num hence we remove letter b from the above step
        - *arr.pop()* retrives the last element in the index eg. b102 => **102 pop() gives 2 which actually denotes the file (col no.)**
        - we again use shift() to get the 0th index now: **for 102 it will be 1 which denote the rank (row no.)**
        - and **a** is assigned **row+col**
        -using the if conditions we **color** the elements where even numbered box will dark and odd numbered box will light




