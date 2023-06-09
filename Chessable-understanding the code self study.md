### first regular chess game.
1. Understanding Javascript 
    - refer 2-game.html and 2-game.css for static design of the 2-player chess game. and script.js for the game
    1. coloring function
        - let's first see coloring function the below code snippet defines the function.
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

    2. insertImage function
        - the below code snippet shows the insertImage function 
        ```
        function insertImage() {
            document.querySelectorAll('.box').forEach(image => {
                if (image.innerText.length !== 0) {
                    if (image.innerText == 'Wpawn' || image.innerText == 'Bpawn') {
                        image.innerHTML = `${image.innerText}<img class='allimg allpawn' src="pieces/${image.innerText}.png"alt="">`
                        image.style.cursor = 'pointer'
                        }
                    else {
                        image.innerHTML = `${image.innerText}<img class='allimg' src="pieces/${image.innerText}.png" alt="">`
                        image.style.cursor = 'pointer'
                    }
                }
            })
        }
        insertImage()
        ```
        - This function is used to insert the image by using the innerText of the **list item** (refer 2-game.html)
        - The first line in definition body selects all the elements which has the class **".box"** and pass each element as such in a array temp and consider each as **image** variable
        - and for every image we define the foreach body
        - If the inner Text's length is not equal to 0 as it can be the text in *<li>* tag in 2-game.html we go in if statement
        - 1. if **image**'s innerText is Wpwan or Bpawn i.e (either a black pawn or white pawn) then,
                change the inner text by adding the image in *<li>* using '${image.innerText}' this will keep the text i.e example **Bpawn** and a img tag with **Bpawn.png** file 
        - 2. Same goes for the other pieces to be added using the text as the file name like Brook, Wqueen etc 

    3. reddish function
        ```function reddish() {
        document.querySelectorAll('.box').forEach(i1 => {
            if (i1.style.backgroundColor == 'cadetblue') {

                document.querySelectorAll('.box').forEach(i2 => {

                    if (i2.style.backgroundColor == 'green' && i2.innerText.length !== 0) {


                        greenText = i2.innerText

                        cadetblueText = i1.innerText

                        cadetblueColor = ((Array.from(cadetblueText)).shift()).toString()
                        greenColor = ((Array.from(greenText)).shift()).toString()

                        getId = i2.id
                        arr = Array.from(getId)
                        arr.shift()
                        aside = eval(arr.pop())
                        aup = eval(arr.shift())
                        a = aside + aup

                        if (a % 2 == 0 && cadetblueColor == greenColor) {
                            i2.style.backgroundColor = '#8F9EB8'
                        }
                        if (a % 2 !== 0 && cadetblueColor == greenColor) {
                            i2.style.backgroundColor = '#C3CDDC'
                        }

                        // if (cadetblueColor == greenColor) {
                        //     i2.style.backgroundColor = 'rgb(253, 60, 60)'
                        // }
                    }
                })
            }
        })
        }   
        ```
        - this function will prevent from capturing same color elements.
        - using i1 we iterate and check each .box element
        - if i1 had bg 'cadetblue' then we take i2 to iterate through all .box element
        - if i2 has color green and text is not null which means a possible move for the piece selected and there might a piece to be captured
        - lets assume @ 202 there is Wpawn and @ 303 there a Wpawn a pawn can take one step diagonal, so 
        hence both have innerText Wpawn
        cadetblueColor using ((Array.from(cadetblueText)).shift()).toString() we get the first letter of the innerText of i1(cadetblue), i2 (green).
        - If both are equal ie. W = W then we will then, we use this condition and also col, row num's sum ie. a if its even put dark blue else light blue. 
    
    4. checkpawn function
        ```
        function checkpawn(){
            document.querySelectorAll('.box').forEach(checkpawn =>{
                id=checkpawn.id
                idnum = parseInt(id.substr(1,4))
                if (checkpawn.innerText == 'Wpawn' && 800<idnum && idnum<809) {
                    checkpawn.innerText = "Wqueen"
                }
                if (checkpawn.innerText == 'Bpawn' && 100<idnum && idnum<109) {
                    checkpawn.innerText = "Bqueen"
                }
            })
        }  
        ```
        - In this function we check whether each element is a pawn or no, if it is then we get its position by passing the id of the box ele.
        -  if Wpawn ranges 800 to 809 i.e eighth row and any col then its promoted to Wqueen
        - similary if Bpawn ranges to 100 to 109 then its promoted to Bqueen 
    
    5. Actual game iterated as foreach **'item'** i.e the item we click on.

    ```
    tog = 1
    document.querySelectorAll('.box').forEach(item => {
    item.addEventListener('click', function () {
    ```
    - we add a event listener click to all .box items
    ```

        // To delete the opposite element

        if (item.style.backgroundColor == 'green' && item.innerText.length == 0) {
            tog = tog + 1
            setTimeout(flip, 800);
        }
        if (item.style.backgroundColor == 'yellow' && item.innerText.length == 0) {
            tog = tog + 1
            setTimeout(flip, 800);
        }

    ```
    - if the background color is green (shows possible move for the piece) and the box has no text
    - tog = tog + 1, after a successful move the board will be flipped using setTimeout(flip,800)
    ```
        else if (item.style.backgroundColor == 'green' && item.innerText.length !== 0) {
            
            document.querySelectorAll('.box').forEach(i => {
                if (i.style.backgroundColor == 'cadetblue') {
                    cadetblueId = i.id
                    cadetblueText = i.innerText
                    
                    document.getElementById(cadetblueId).innerText = ''
                    item.innerText = cadetblueText
                    coloring()
                    insertImage()
                    tog = tog + 1
                    setTimeout(flip, 800);
                    checkpawn()
                    insertImage()
                    checkchecks()
                }

            })
        }
    ```
    - The above else statement check if there is a piece to be captured if yes then selected piece is cadetblueId we clear the innerText be setting it '' (null)  and set item's inner text i.e the captured piece as cadetblueId innerText and then filp the board

5. Function whosTurn, which will have all piece movement of each color the toggle variable will be either 'W' or 'B', for each piece we check who's turn.

    ```
    function whosTurn(toggle) 
    ```
    1. Pawn
    ```
    // PAWN
    if (item.innerText == `${toggle}pawn`) {
        checkchecks()
        if (tog % 2 !== 0 && aup < 800) {
            // For white side
            if (aup == 200) {
                //for pawn can move two squares on first move
                if (document.getElementById(`b${a + 200}`).innerText.length==0 && document.getElementById(`b${a+100}`).innerText.length == 0) {
                    document.getElementById(`b${a + 200}`).style.backgroundColor = 'green'
                    }
                }
                if (document.getElementById(`b${a + 100}`).innerText.length == 0) {
                    document.getElementById(`b${a + 100}`).style.backgroundColor = 'green'
                }
                if (document.getElementById(`b${a + 100 + 1}`) && document.getElementById(`b${a + 100 + 1}`).innerText.length!== 0) {
                    document.getElementById(`b${a + 100 + 1}`).style.backgroundColor = 'green'
                    }
                    if (document.getElementById(`b${a + 100 - 1}`) && document.getElementById(`b${a + 100 - 1}`).innerText.length !== 0) {
                        document.getElementById(`b${a + 100 - 1}`).style.backgroundColor = 'green'
                        }
                    }

                if (tog % 2 == 0 && aup > 100) {
                    // For black side
                    if (aup == 700) {
                        //for pawn can move two squares on first move
                        if (document.getElementById(`b${a - 200}`).innerText.length == 0 && document.getElementById(`b${a - 100}`).innerText.length == 0) {
                            document.getElementById(`b${a - 200}`).style.backgroundColor = 'green'
                        }
                    }
                    if (document.getElementById(`b${a - 100}`).innerText.length == 0) {
                        document.getElementById(`b${a - 100}`).style.backgroundColor = 'green'
                    }
                    if (document.getElementById(`b${a - 100 + 1}`) && document.getElementById(`b${a - 100 + 1}`).innerText.length !== 0) {
                        document.getElementById(`b${a - 100 + 1}`).style.backgroundColor = 'green'
                    }
                    if (document.getElementById(`b${a - 100 - 1}`) && document.getElementById(`b${a - 100 - 1}`).innerText.length !== 0) {
                        document.getElementById(`b${a - 100 - 1}`).style.backgroundColor = 'green'

                    }
                }

                item.style.backgroundColor = 'cadetblue'
                reddish()
                    
            }
    ```


