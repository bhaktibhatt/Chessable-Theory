1. first regular chess game.
    - refer 2-game.html and 2-game.css for static design of the 2-player chess game. 
    - Understanding Javascript 
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
                    color.style.backgroundColor = '#8F9EB8'
                    }
                if (a % 2 !== 0) {
                    color.style.backgroundColor = '#C3CDDC'
                    }
            })
        }
        coloring()
```
