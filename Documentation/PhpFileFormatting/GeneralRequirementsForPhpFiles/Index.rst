.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../Includes.txt


.. _general-requirements-for-php-files:

General requirements for PHP files
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^


PHP tags
""""""""

Each PHP file in TYPO3 must use full (as opposed to short) PHP tags.
There must be exactly one pair of opening and closing tags (no closing
and opening tags in the middle of the file). Example::

   <?php
           // File content goes here
   ?>

There must be no empty lines after the closing PHP tag. Empty lines
after closing tags break output compression in PHP and/or result in
AJAX errors.


Line breaks
"""""""""""

TYPO3 uses Unix line endings (:code:`\n`, PHP :code:`chr(10)`). If
a developer uses Windows or Mac OS X platform, the editor must be
configured to use Unix line endings.


Line length
"""""""""""

Very long lines of code should be avoided for questions of
readability. A line length of about 130 characters (**including**
tabs) is fine. Longer lines should be split into several lines whenever
possible. Each line fragment starting from the second must - compared
to the first one - be indented with one tab character more. Example::

   $rows = $GLOBALS['TYPO3_DB']->exec_SELECTgetRows('uid, title', 'pages',
           'pid=' . $this->fullQuoteStr($this->pid, 'pages') . $this->cObj->enableFields('pages'),
           '', 'title');

or even better for readability::

   $rows = $GLOBALS['TYPO3_DB']->exec_SELECTgetRows('uid, title',
           'pages',
           'pid=' . $this->fullQuoteStr($this->pid, 'pages') . $this->cObj->enableFields('pages'),
           '',
           'title'
   );

Comment lines should be kept within a limit of about 80 characters
(**excluding** tabs) as it makes them easier to read.


Notes
~~~~~

- Tabs are considered to be 4 spaces wide.

- When splitting a line, try to split it at a point that makes as much
  sense as possible. In the above example, the line is split between two
  arguments and not in the middle of one. In case of long logical
  expressions, put the logical operator at the beginning of the next
  line, e.g.::

   if (
       $GLOBALS['TYPO3_CONF_VARS']['SYS']['curlUse'] == '1'
       && preg_match('/^(?:http|ftp)s?|s(?:ftp|cp):/', $url)
   ) {


Whitespace and indentation
""""""""""""""""""""""""""

TYPO3 uses tab characters to indent source code. One indentation level
is one tab.

There must be no white spaces in the end of a line. This can be done
manually or using a text editor that takes care of this.

Spaces must be added:

- on both sides of string, arithmetic, assignment and other similar
  operators (for example :code:`.`, :code:`=`, :code:`+`, :code:`-`,
  :code:`?`, :code:`:`, :code:`*`, etc)

- after commas

- in single line comments after the comment sign (double slash)

- after asterisks in multiline comments

- after conditional keywords like :code:`if (` and :code:`switch (`

- before conditional keywords if the keyword is not the first
  character like :code:`} elseif {`


Character set
"""""""""""""

All TYPO3 source files use the UTF-8 character set without byte order
mark (BOM) since version 4.5. Encoding declarations like
:code:`declare(encoding = 'utf-8');` must not be used. They might lead
to problems, especially in :code:`ext_tables.php` and
:code:`ext_localconf.php` files of extensions, which are merged
internally in TYPO3 CMS. Files from third-party libraries may have
different encodings.
