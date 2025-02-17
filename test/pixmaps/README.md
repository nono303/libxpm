The pixmaps under this directory are used as test cases for several tests.
The tests iterate over all files in each directory, so new test cases can be
added by just adding a file there, adding it to the `EXTRA_DIST` list in
`test/Makefile`, and adding a note here to help us remember what each test case
covers.  Please make sure all pixmaps are appropriately licensed.

For details on the different format types, see xpmDataTypes in `src/data.c`,
<https://en.wikipedia.org/wiki/X_PixMap>, and
<http://fileformats.archiveteam.org/wiki/XPM>.

good
----

Those under the `good` subdirectory are expected to work and
return XpmSuccess when parsed.

A subset of these are specifically chosen/designed to test various things:

- plaid-v3.xpm - copy of the sample XPM file from pg. 10 of `doc/xpm.PS.gz`,
  in XPM version 3 format

- plaid-v1.xpm - alternate version of plaid.xpm in XPM version 1 format

- plaid-v2.xpm - alternate version of plaid.xpm in XPM version 2 "natural" format

- plaid-lisp.xpm - alternate version of plaid.xpm in XPM Version 2 Lisp format

- jigglymap.xpm - transparent background

Other pixmaps in this directory are a selection of real world XPM files
with a variety of sizes & numbers of colors.

invalid
-------

Those under the `invalid` subdirectory are expected to fail and
return XpmFileInvalid when parsed.

- doom.xpm - This file is originally from
  <http://scary.beasts.org/misc/doom.xpm>.
  It is a test case for the stack-based overflow in xpmParseColors in
  CVE-2004-0687 as described in
  <https://security.appspot.com/security/CESA-2004-003.txt>.

- doom2.xpm - This file is originally from
  <http://scary.beasts.org/misc/doom2.xpm>.
  It is a test case for the stack-based overflow in ParseAndPutPixels
  and ParsePixels in CVE-2004-0687 as described in
  <https://security.appspot.com/security/CESA-2004-003.txt>.

- invalid-type.xpm - This file has an invalid XPM version 2 type header

- no-contents.xpm - This file has a valid header but no contents

- unending-comment-c.xpm - This file has a C comment block without the
  closing "*/" to test for CVE-2022-46285

- zero-width.xpm & zero-width-v1.xpm - These files declare a width of 0
  and a height of nearly UINT_MAX, to test for CVE-2022-44617

- corrupt-colormap.xpm - This file was generated by the clang libfuzzer,
  and serves as a test for CVE-2023-43789

- width-overflow.xpm - This file was provided by Yair Mizrahi of
  the JFrog Vulnerability Research team as a test for CVE-2023-43787.
  Its width causes an integer overflow when multiplied by a depth of 4 bytes
  (32-bits) when using 32-bit ints.

no-mem
------

Those under the `invalid` subdirectory are expected to fail and
return XpmNoMemory when parsed.

- oversize.xpm - This file specifies more pixels than can be mapped in
  a 64-bit address space that already has programs & libraries mapped in.

other
-----

Those under the `other` subdirectory don't fit cleanly in any of the above
categories, and may be valid for some uses but not others, and thus can't be
easily used in the current test framework, but are still interesting cases.

- overflow-stackexhaustion.xpm - This file was provided by Yair Mizrahi of
  the JFrog Vulnerability Research team as a test for CVE-2023-43786.
  It is a valid XPM file, but is larger than fits into an X Pixmap, so
  should pass with many functions, but fail when used with sxpm or
  anything that calls through to xpmCreatePixmapFromImage().
