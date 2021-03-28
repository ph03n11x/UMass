# Details:

Solves: 12

Do you like my dollar store haul?

Hint: No, there's nothing weird with the EXIF data.

Team: K3RN3L4RMY

## Write up:

```Before we start I want to give huge shoutout to my teammates, without them this challenge would remain unsolved```

At the beginning we were given only one picture

![clue](./Photos/clue.jpg)


First I tried to do binwalk but nothing showed up. So I almost tried every possible steg tool, zsteg, exiftool, stegsolver but nothing worked. After consulting with my teammates we got an idea that might be somehting about image itslef. So we started looking at soldiers. After a lot of rabbit holes and fails we managed to get the flag. We came to conclusion that if it's two soldiers per character and ascii values then it's likely to use hex system so can we make 16 varieties on the soldiers. we can look at the first as it uses the same colour soldier with the same pose. So we have 42 soldiers, and most likely 2 soldiers would possibly decode a character, expect ascii ---> hex most likely. Later after that, to check this theory by checking first few soldiers for consistency with UMASS{. So SS should repeat. And U = 55 so that one should have two soldier the same. Then it's filling out the chars we know
So UMASS{ and } at the end
Then we can use the soldiers we now know to fill in some others.

After digging and getting hex values we finnaly created script that got us all possible flags. 

```py
a = "55 4D 41 53 53 7B 6X 66 6X 5Y 74 3Z 76 5Y 73 3Z 6X 6W 34 73 7D"
chars_left = '0289ACEF'

N = len(chars_left)
for i in '289ACEF':
    for j in '289AF':
        if j==i:
            continue
        for k in '0289':
            if k==i or k==j:
                continue
            for l in '289ACEF':
                if l==i or l==j or l==k:
                    continue
                op = a.replace('X',i).replace('Y',j).replace('Z',k).replace('W', l)
                temp = op.split(' ')
                ans = ''
                for c in temp:
                    ans+=chr(int(c,16))
                print(ans)
```

After This we noticed that one of our Hex values is not good so we replaced it and got thefinal flag which is :

`UMASS{lfl_t0v_s0lj4s}` 


