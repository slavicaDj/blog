## Welcome to my Outreachy blog!

My name is Slavica and I'm Outreachy participant for December-March 2018/19 round.
In the next three months I'll be working on Git's project "Turn `git add -i` into built-in" 
with Johannes Schindelin as my mentor.
I am final year Computer Science student, and this is my first time contributing to open-source. 
I've always loved programming and I'm honored having opportunity to participate in such project.
On this blog, I will be publishing posts weekly about my experience. I hope that would benefit 
future applicants and spread the word about Outreachy.  
  
  
  
### How I applied to Outreachy

I've first heard of Outreachy two years ago from my friend who volunteered from Mozilla.
This round was right moment to apply, since I'm almost done with my college.  

**My motivation**  
* learning new things
* working with experts
* meeting international friends
* and possibly traveling!  

**How it went**   
All neccessary information was on Outreachy site: [https://www.outreachy.org/](https://www.outreachy.org/)
It says all about projects, deadlines, prerequisites, mentors, communication channels, etc.
There I picked my project, found out about Gitter, contacted mentor - everything was pretty straightforward.  
And yes, I think that I have the greatest mentor ever - from the beginning, he is more than helpful, answering all
questions (and the nooby ones too), patient, calm, and on top of that one of the core Git contributors!  
My first contribution was based around client's request I found on git mailing list. This client wanted to use 
`git stash` command without being forced to configure user.name and user.email.
I do have experience with using git, shell scripts, C, etc, but this is something I worked in some period of time, 
and I sure needed some recalling. Also, I had to learn how to communicate through mailing list to send patches and replies.
I was unsecure at moments, but I figured it all out, and learned a lot along the way!

**Should you apply?**  
Yes of course! I would like to encourage everyone who is hesitant whether to apply or not: go for it! If you are 
passionate about what you do and eager to learn, don't be afraid about things you don't know.
  
  
  
### First steps

It's been two weeks since I'm working on my project "Turn `git add -i` into built-in". The project is essentially about translating 
`git add -i` command from Perl script to C. As I already described, I made my contribution while I was applying for project, but that was just just "scratching the surface". Now I am able and commited to truly explore Git. I am learning something new every single day on this internship, and this is just the beginning.  
These two weeks were about applying patch series from (former) Git contributor Daniel, resolving merge conflicts, fixing build errors, some coding, but most of the time getting myself familiar with the code. Although I didn't do much in this stage, it was interesting to poke around, explore and put pieces of puzzle together.  
Perhaps the most interesting moment was enabling TTY on Windows.  
And here goes the story. I was testing the code I wrote, and since I wanted to make sure output it gives is the identical to expected, that meant testing output color as well. My mentor introduced me with function `test_decode_color` that will do that. (Neat function, I thought). Using this function requires that test has TTY ticked. This esentially means just writing TTY before test name:
```
test_expect_success TTY 'show help from add--helper' '
  ...
```
But, it didn't work. It said TTY is missing. I thought I've done something wrong, and when I heard from my mentor he realized that it's because TTY is not enabled on Windows. I thought: that's it, I need to move on Linux, problem solved. I didn't even consider that this issue can be addressed.  
After few minutes, my mentor said that we can "patch the code so that an environment variable, say, GIT_TEST_PRETEND_TTY can force Git to think that it is talking to a TTY." I was truly amazed. In the end, all it took were few lines (three to be exact). It would never occur to me that "inconvenience" like this one could be solved, much less in a few minutes. This is thinking outside of the box.  
  
  
  
### Everybody struggles
  
This is the post for everyone out there who is struggling and thinks they're not good enough because of it. Third week of internship was about letting others know that we all have moments when we are stuck. Intens and mentors wrote about their experience on public chat, and this is mine:
> I usually struggle to ask questions that are not "smart enough". But I must admit Outreachy helped me do this more often. For example, in the first days of internship, I had to use shell script to apply series of patches. I just needed to supply it with link. I did that, but with spare brackets, and of course, it didn't work. When I asked mentor about this, he realized problem, obviously. 
> This was painfully simple to solve, but very difficult to ask. I was a bit embarrassed, but after this I find it a lot easier to ask for help.

I usually don't share similar experiences, especially on public chats, but Outreachy community encouraged me to do so. 
Important thing is not to see this as something abnormal. It is good idea to take a break, relax, and ask for help. Everyone is having difficulties. The problem is, we only see one's success - we don't even consider how much they struggled. And just think: is it possible to learn something completely new, to wrap your head around concepts you never heard of, to grow and never get stuck along the way?



### More about Git and my project
  
As I said in previous posts, I am Git intern via Outreachy. For those who haven't heard of Git (although you most probably did if you do programming): it is distributed version-control system, which enables programmers to efficiently share, maintain (its history) and experiment with their code. Word "distributed" in description stands there because:
> every developer's working copy of the code is also a repository that can contain the full history of all changes.[1]  

This means there is not one place where all code is being kept.  
  
Git community's job is maintaining Git and making it more awesome (like it's not already:)): upgrading, answering user's questions, fixing existing bugs etc.. And from what I can see, most of the Git's contributors are highly skilled and do no less then amazing. There is so much to learn from them. When I was first applied for Git, during that time, I was merely trying to code, but to get to feel how community works, what are coding guidelines, how to communicate, how to make patches... 

Now I am working on project "Turn `git add -i` into built-in": `git add -i` is one of the git's commands. It is somewhat similar to `git add`, which purpose is to tell git to track file(s) you added with that command. But, the difference the two is that the former is in **interactive** mode.  For example, if you run `git add -i`, you will get menu like this [2]:
```
  *** Commands ***
      1: status       2: update       3: revert       4: add untracked
      5: patch        6: diff         7: quit         8: help
    What now> 1
```
You can choose between the options either by typing a number, or letters that can uniquely select one of them.  
So, what do I do? I am turning this command into built-in. Right now, `git add -i` is written in Perl script.  
I need to re-write it in C. Why do I do that? Because in that way, we achieve better portability, performance, and all the good reasons.  
And since I mentioned selection one of the `git add -i` options, at the very this point on my internship, I'm trying to "translate" Perl script's way of dealing with unique prefixes into C. Besides doing its job, this translated part needs to do it with reasonable complexity and without overheads.  

I am so grateful to be part of Git's community and work on this project. So far, I've learned to use Git much better: rebasing, squashing, splitting, amending commits -- all the things that I wasn't too familiar with before. Also, I've found out more about Git's codebase.  
For example, test suite -- where to write tests (there are interesting rules about this), get to know syntax, use integrated commands.  
Code is written by high standards. I've learned (or still trying:) to write code respecting them and other established rules. All things matter, including how you use spaces and tabs.  
Also, not everything is explained in comments: that's why command `git grep` introduced to me by mentor was very helpful. Said command searches through all files and find all occurrences of specified string. I used it every time I wasn't clear on how to use some structure, command, or constant. Of course, my mentor is always there to help if I can't do it out on my own. :)  
This was interesting way to figure things out, and I didn't have chance to do it before.  

And in the beginning, almost everything seemed confusing and unfamiliar. Git is a huge project, and I took my time getting to know it. But I wouldn't like the other way. I know that if I struggle, put a lot of effort, I am on the right path. That only means I will grow and learn more. The most important thing here is to never stop wondering, be eager and excited. That way everything else will sort out.

[1][https://www.atlassian.com/git/tutorials/what-is-git](https://www.atlassian.com/git/tutorials/what-is-git)  
[2][https://git-scm.com/docs/git-add](https://git-scm.com/docs/git-add)
