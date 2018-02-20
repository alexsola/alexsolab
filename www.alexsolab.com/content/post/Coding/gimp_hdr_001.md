---
title: "GIMP: HDR pictures mixing 3 images"
date: 2016-10-10T20:10:58+01:00
draft: false
---

![HDR Final](/img/gimp_hdr_intro.jpg "Test picture taken in Luxemburg")

I wanted to understand how HDR photography works so I thought the best way to fully understand it is to try to code something to apply the algorithm and see the results. As GIMP has a very powerful framework for scripting, I thought this is a good platform to do it. GIMP support 2 languages: Python and Scheme. To make things more interesting, and go back to the days of Lisp programming, I chose Scheme for this. Follows the requirements for the project:

* Must be written for GIMP
* Must be written in Scheme
* Must take three images
* Must output one image
* Must keep all three images in layers
* Must be possible to adjust levels individually
* The result must be an HDR image

As HDR, we understand High Definition Range. The idea is to make 3 pictures:

* one with good/normal exposure, considered the base for the image. Also called the middle one.
* a second one overexposed, from which we will take only the dark places of the middle one. The overexposed image is also called the High one.
* a third one infraexposed, from which will take the bright parts of the middle one. The infraexposed image is also called the Low one.

Based on this premises and definitions, I coded a scrip in Scheme which creates a new image based on three input images. To achieve the algorithm definition and select the dark and the bright sides of the pictures, we use masks. To create the mask for bright sides, we just desaturate the corresponding image and raise a bit the levels. Use this result as the mask for the infraexposed picture. And the inverted one for the overexposed picture. The result are as follows:

![gimp hdr 3 exposures](/img/gimp_hdr_test001.png "Final result, super-expose, normal-expose and infra-exposed")

This script, is no way perfect, still needs some improvements. At least, needs some treatment to remove the ghosts. But so far, is a good start point.

```
; FUNCTION REGISTRATION
(script-fu-register
    "script-fu-hdr3"                                ;func name
    "HDR Stack of 3 Images"                         ;menu label
    "Creates a new image from\
Stacking three pictures as layers\
 and adding masks."                                 ;description
    "Alex Sola"                                          ;author
    "copyright 2015, Alex Sola"                          ;copyright notice
    "September 30, 2015"                                 ;date created
    ""                                                   ;image type that the script works on

;    SF-DIRNAME    "Dir of images"  "/var/tmp"
    SF-FILENAME   "Mid Exposured Image"  "/Users/Noctrum/Documents/Proyectos/Schwangau-House001_HDR_001/JPG_Originals/SchwangauHouseHDR-2.jpg"
    SF-FILENAME   "Under Exposured Image"  "/Users/Noctrum/Documents/Proyectos/Schwangau-House001_HDR_001/JPG_Originals/SchwangauHouseHDR-1.jpg"
    SF-FILENAME   "Over Exposured Image"  "/Users/Noctrum/Documents/Proyectos/Schwangau-House001_HDR_001/JPG_Originals/SchwangauHouseHDR-3.jpg"
  )
(script-fu-menu-register "script-fu-hdr3" "/File/Create/Photo-toolbox")

; SCRIPT BODY
(define
        (script-fu-hdr3 midExpose underExpose overExpose)
        (let*
             (
		(useless 0)
		(theMidImage)
		(theOverLayer)
		(theUnderLayer)
		(maskOverLayer)
		(maskUnderLayer)
             )

	(set! theMidImage (car (gimp-file-load RUN-NONINTERACTIVE midExpose midExpose)))
        (gimp-display-new theMidImage)
	(set! theUnderLayer (car (gimp-file-load-layer RUN-NONINTERACTIVE theMidImage underExpose)))
	(set! theOverLayer (car (gimp-file-load-layer RUN-NONINTERACTIVE theMidImage overExpose)))
	(gimp-layer-add-alpha theUnderLayer)
	(gimp-layer-add-alpha theOverLayer)

	(gimp-image-insert-layer theMidImage theUnderLayer 0 -1)
	(gimp-image-insert-layer theMidImage theOverLayer 0 -1)

	(set! maskUnderLayer (car (gimp-layer-create-mask theUnderLayer ADD-COPY-MASK)))
	(gimp-layer-add-mask theUnderLayer maskUnderLayer)
	(set! maskOverLayer (car (gimp-layer-create-mask theOverLayer ADD-COPY-MASK)))
	(gimp-layer-add-mask theOverLayer maskOverLayer)
	(gimp-invert maskOverLayer)
;	(gimp-image-set-active-layer theMidImage maskUnderLayer)
;	(drawable (car (gimp-image-get-active-layer theMidImage)))
;	(gimp-desaturate-full (maskUnderLayer DESATURATE-LUMINOSITY))
        (gimp-image-clean-all theMidImage)
        )
)
```
