+++
title = "recursion"
date = 2008-10-26
description = "fun with recursion"
authors = []
draft = false

[taxonomies]
tags=[ "software-development", "tool" ]
+++

After writing the code below recently, I searched out a few cohorts at work to share the joy, but it was late and no one was around...    
     
      def makeHierarchicalFolderList( folder_object_list, return_list=[], indent='' ):    
           '''    
           - Called by: views.uploader3()    
           - Purpose: to create a list of community-folders (for upload form) with indents indicating hierarchical relationship. Will likely be replaced by better user-interface.    
           '''    
                                   
           for folder in folder_object_list:    
                folder.name = '%s%s' % ( indent, folder.name )    
                return_list.append( folder )    
                    
                # check for children    
                children_count = folder.communityfolder_set.all().count()    
                    
                # handle check-results    
                if children_count == 0:    
                     pass    
                else:    
                     children_object_list = folder.communityfolder_set.all()    
                     indent = indent + '-'    
                     makeHierarchicalFolderList( children_object_list, return_list, indent=indent )    
                     indent = indent[1:] # since we're at the end of a processing chain, remove the indent    
                         
           return return_list    
                    
           # end def makeHierarchicalCommunityFolderList()    
     
 What enthused me so was the line a few up from the bottom, where I call the very function in which this line resides. This is called recursion. There's a wonderful slightly mysterious inverted mobius-strip-like quality to recursion, except that if done right, processing doesn't continue on forever.     
     
 The code above neatly meets the needs of a project I'm working on: to prepare a hierarchical listing of folders. Not shown is an initial step in which a query is made for a user-specific list of 'top-level' folders -- that is, folders which do not have a parent folder. For each folder in this list, the folder is first appended to a sort of global list-of-folders-to-return. Then a check is made to see if the folder has any children. If so, those child-folders are selected, and passed to the function itself. So for each top-level folder, a processing-chain begins that might be very, very long, or might be very short. But each processing-chain does terminate, shifting to examine the next sibling folder, and, when there are no more sibling-folders in the lowest-level generation, shifting back upward a generation to examine and process the next sibling-folder.    
     
 I use recursion infrequently enough that it sort of gets buried in my toolbox. I forget about it and from habit reach for other tools first that often do the looping job well-enough. Utilizing looping-logic is a fundamental part of programming. Where a built-in looping structure doesn't directly solve looping needs, I most often use a Controller-pattern solution to a looping challenge. That is, I'll have a controller block of code prepare a list of items that need to be looped through, and perhaps set some variables to hold the results of processing, and then call a separate function that handles the actual looping. Sometimes for more complex situations the called looping code can itself call another separate block of looping code. So it is possible to handle some situations, for which recursion might be ideal, with other techniques. But not all situations -- when my usual looping implementation begins feeling overly complex, that's often a sign to root around and dust off the recursion tool.    
     
 Despite some left-over 1960's geek-stereotypes about programming being a boring left-brain process, there can be elegance and deep beauty in programming. There are numerous ways to approach and solve a challenge, any of which may work 'well-enough'. Good programmers strive for solutions that are simplest and clearest, and when the right technique lends itself to beautifully simple code, one feels like an artist.