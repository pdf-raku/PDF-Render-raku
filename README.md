PDF-Render-Simple
===========

Description
-----------

Simple rendering of accessible PDF from tagged-PDF like rendering trees.

Synopsis
--------

```raku
use PDF::Render::Simple;

my %role-map = (
    'U' => :Span[:TextDecorationType<Underline>],
    'X' => :Index[],
);

my Pair:D $pdf-ast =
    :Document[ :Lang<en>,
        :H1["A basic Test Document"],
        :P["This text is ", :Em["italic"], "."],
        :P["This text is ", :Strong["bold"], "."],
        :P["This text is ", :U["underlined"], "."],
        :P["This text contains a link to ", :Link[:href("http://www.google.com/"), "google"], "."],

        "#comment" => " a real-world sample, converted from Supply.rakudoc",
        :P["A tap on an ", :Code[:X[ "on demand"]]," supply will initiate the ",
           "production of values and tapping the supply again may result in a new set of values.",
           "For example, ", :Code[:X["Supply.interval"]], " produces a fresh ",
           "timer with the appropriate interval each time it is tapped."],
     ];

my PDF::Render::Simple $renderer .= new: :%role-map;
my PDF::API6 $pdf = $renderer.render($pdf-ast);
$pdf.save-as: "example.pdf";
```

Description
-----------
This module supports rendering of simple tagged PDF text documents.

It is designed to easily translate from classic Raku POD or markdown
formats, or to be directly used to generate simple text PDF documents.
