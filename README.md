# g3jafar-a3
Repository worked on for Bug 1247190: https://github.com/jafar25/loop
# Bug Choices

Initially, I had picked bug 1205569 ( https://bugzilla.mozilla.org/show_bug.cgi?id=1205569 ), which seemed interesting to me, since someone who couldn't read any Right-to-Left languages had attempted it and was not able to complete a patch. The bug appears when Firefox is installed in a Right-to-Left language environment, such as Arabic. The developer console icons would appear at the wrong positions.

![alt tag](https://bug1205569.bmoattachments.org/attachment.cgi?id=8662229)

# Quick summary of the fixes for Bug 1205569

It turned out that once it's possible to simulate RTL formatting, a simple css margin fix provided acceptable output:

Before:

![alt tag](https://github.com/csc302-2016-spring/g3jafar-a3/blob/master/screenshots/rtl.before.png)

After:

![alt tag](https://github.com/csc302-2016-spring/g3jafar-a3/blob/master/screenshots/rtl.after.png)

Unfortunately, the bug was put on hold because the developers were planning on replacing this interface design.

At the same time, I had been assigned another bug, 1247190 ( https://bugzilla.mozilla.org/show_bug.cgi?id=1247190 ), due to a misunderstanding with the CDF id spreadsheet, when I had commented on the bug before another student, who also wanted the same bug, who wrote it on the spreadsheet before I did. I chose to back down and let them have it, but mozilla still assigned it. Upon my original bug being put on hold, I chose to do this one once the other student had changed their chosen bug anyway.

# Bug 1247190

The problem here was simple. Mozilla is working on a new add-on, called "Hello." It is also code-named Loop, and it allows quick video calling and similar features to Skype, from within the browser by simply sharing a link. Since it is still a new add-on, they had recently switched to github and changed their path retrieval. The boolean useDesktopPaths was no longer needed and should be removed.

It's a simple code search and removal.

The important parts of diagnosis were to fork their repository and run tests that ensure the same results were obtained before and after removal, since there is no actual malfunction.

I forked the repository and made a local branch

![alt tag](https://github.com/csc302-2016-spring/g3jafar-a3/blob/master/screenshots/screenshot.1.png)

Oddly enough, there were errors upon initial download and build. After ensuring the right version of nodejs was installed and all necessary libraries were available, Loop still produced the following errors when building or testing:

![alt tag](https://github.com/csc302-2016-spring/g3jafar-a3/blob/master/screenshots/screenshot.2.png)

However after more consideration and testing, it seemed not as odd, as there were still patches of Loop being written, and the files it was asking for weren't in the github repository to begin with yet.

# Testing

I made a few changes to the files I wanted to modify for the bug to purposely produce errors that ensure tests for them were still run. Since they were being tested, everything was ready for the removal tests before submission.

I removed the uses of useDesktopPaths in the files found with grep and ran "make build" and "make test" on the repository. It produced no new errors. The patch was ready to be made.

I ensured no trailing spaces or bad formatting was in the patch before uploading to Bugzilla. Upon being reviewed by a mentor, it was deemed ready for a push.
