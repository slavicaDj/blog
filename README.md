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
I need to re-write it in C. Why do I do that? Because in that way, we achieve better portability, performance, and for all good reasons.  
And since I mentioned selection one of the `git add -i` options, at the very this point on my internship, I'm trying to "translate" Perl script's way of dealing with unique prefixes into C. Besides doing its job, this translated part needs to do it with reasonable complexity and without overheads.  

I am so grateful to be part of Git's community and work on this project. So far, I've learned to use Git much better: rebasing, squashing, splitting, amending commits -- all the things that I wasn't too familiar with before. Also, I've found out more about Git's codebase.  
For example, test suite -- where to write tests (there are interesting rules about this), get to know syntax, use integrated commands.  
Code is written by high standards. I've learned (or still trying:) to write code respecting them and other established rules. All things matter, including how you use spaces and tabs.  
Also, not everything is explained in comments: that's why command `git grep` introduced to me by mentor was very helpful. Said command searches through all files and find all occurrences of specified string. I used it every time I wasn't clear on how to use some structure, command, or constant. Of course, my mentor is always there to help if I can't do it out on my own. :)  
This was interesting way to figure things out, and I didn't have chance to do it before.  

And in the beginning, almost everything seemed confusing and unfamiliar. Git is a huge project, and I took my time getting to know it. But I wouldn't like the other way. I know that if I struggle, put a lot of effort, I am on the right path. That only means I will grow and learn more. The most important thing here is to never stop wondering, be eager and excited. That way everything else will sort out.

To condense everything in this post, I'll mention things that I would say to my past-self, when I first applied to Outreachy:
* Believe in yourself, you are up to the task!
* Please ask more questions, no matter how simple
* Don't be afraid of failure
* Don't think less of yourself if you don't know or understand something, you will learn it
* Don't stress over code reviews, you will get your first patch merged eventually

[1][https://www.atlassian.com/git/tutorials/what-is-git](https://www.atlassian.com/git/tutorials/what-is-git)  
[2][https://git-scm.com/docs/git-add](https://git-scm.com/docs/git-add)

### Modifying expectations

In the application process, all Outreachy participants should consult their mentor and plan the project timeline. This week, we're supposed to reflect on that timeline, and say what things went different than expected. I'm going to answer some questions that were given as guidance for this week blog post.

**What was your original internship project timeline?**  
04.12.2018. 
First things first: the most successful strategy to convert a script to a built-in appears to introduce a built-in helper first, extracting functionality from the script and then calling the helper from the script.
A good example to follow is 3d5ec65. It introduces a new helper, written in C, and we should do the same, following the same naming convention `git-stash--helper`: we should call our helper `git-add--helper`. I would even recommend introducing the helper without any functionality first, just to get those changes out of the way: new file builtin/add--helper.c, then the associated changes in `Makefile`, `builtin.h`, `git.c` and `.gitignore`.

05.12.2018. - 08.12.2018.
Now let's look at https://github.com/git/git/blob/v2.19.1/git-add--interactive.perl. There is already some logical code flow structuring by grace of having functions (or "subroutines", as Perl calls them, memorialized via the keyword sub). Let's see whether those functions give us a good structure for the conversion to follow.
The first function is called `run_cmd_pipe` and is clearly too low-level to be moved to a built-in. Same for `refresh`. And maybe also for `list_untracked`.
`is_initial_commit` is used more than once, but let's see whether the first user, `get_diff_reference` is a good candidate for a first code move to the built-in helper. It clearly needs `get_empty_tree`, which is also used in `diff_cmd`. But yes, it looks as if that would make for a fine start.
Since it is the first real code move, I would probably give this 1-3 days to get right.

09.12.2018 - 23.12.2018.
`list_modified` looks like a logical next task. This is a bit complex a function, and it does a lot of text processing of the output of diff-index and diff-files. That would have to be done differently in a built-in, of course, as it would have to call the underlying APIs instead and produce different output than diff-index and diff-files.
I think I would give this a good 2 weeks to get right.

24.12.2018 - 21.01.2019.
The `find_unique` function looks like it operates on Perl data structures, which would be hard to convert to C individually, as you would have to de-serialize the data structures into a command-line (or into a stream that is fed to the stdin of the built-in command). So I think it has to be done as part of moving the code of the only user, `list_and_choose`.
Same goes, unfortunately, for `find_unique_prefixes`.
And as `update_trie` is only used by `find_unique_prefixes`, the same goes for that function.
`list_and_choose` is also the only caller of `highlight_prefixes`, which in turn is the only user of `is_valid_prefix`. And it is a function that outputs color, i.e. it has to have a notion whether this command really is run connected to an interactive terminal (as opposed to connected to another process via pipes).
So `list_and_choose` and its callees are the next task, and it is big. 3-4 weeks, I would guesstimate, maybe even more. 

22.01.2019. - 08.02.2019.
There are a couple of `*_cmd` commands after that, which seem to basically rely on `list_and_choose` and then do only minimal things on top. Those functions would be the next tasks. Probably a couple of days, each, `revert_cmd` maybe a bit more (judging by its size).

08.02.2019. - 04.03.2019.
Then there are a lot of patch parsing/reassembling functions up until (and including) `reassemble_patch`, and they seem to pass around Perl arrays. I think that this is basically all needed for `edit_hunk_manually`, but I have not analyzed it all that well yet.
`prompt_single_character` will be tricky; I do not think there is a POSIX way to do that, so we will have to figure something out that is not too un-portable.
This concludes the timeline so far, as far as my best guess of a realistic one goes, and we'll have to take it from there, when we reach that point.

**What goals have you met?**  
I've done everything like planned in timeline, except for `list_and_choose` function, which according to my timeline should've been finished four days ago. I've actually wrote initial draft of that function, but it needs more polishing, refractoring, etc.

**What have you accomplished in the first half of your internship?**  
The most important thing for me is that I learned so much, and I'm still learning. I also got more confident when writing code and asking questions. As for project timeline, I'm not sure if I'm going to do everything planned, but I hope I'll get close to it.

**What project goals took longer than expected?**  
One of the goals of project was to translate function `find_unique_prefixes`. In the original version, this function relied on trie structure. First I looked around the codebase to find such implementation, and there were two, but none of them weren't what I really needed, so I asked my mentor for help and he suggested different approach. It took me time to realize and implement it. I asked my mentor multiple times to help me with it. I really didn't anticipate I will need to work so much on this function.

**Why did those project goals take longer than expected?**  
I'm not sure why I had so much problem with function I described in previous question. It wasn't anything too complicated, but I kept hitting roadblock and failing to understand how to do it. When I finally finished, it looked quite straightforward. Whatever the reason was, it's good I had my mentor's help and I'm truly grateful for that.

**What would you do differently if you were starting the project over?**  
I would probably stress less and ask more questions.

**Which original goals needed to be modified?**  
Since I used patch series of another Git contributor as head-start, I didn't have to write some portion of the code for the project, but since patches were outdated, I needed to work on applying them, adapting them, fixing merge conflicts, etc. Also, since I didn't used trie  in that `find_unique_prefixes` function, I didn't translate `update_trie` function as well.

**What is your new plan for the second half of the internship?**  
Since I'm pretty much following initial plan and it seems appropriate, I don't have new one at this point. I am few days late according to the timeline, but that is totally fine, since timelines are usually not strictly followed, and one usually gets stuck in the way.
