# Introduction #

This is a simple class for compressing and extracting files. It works depend on minizip, which is a open source zip format library. And it’s included in the attachment.

The major class name is ZipArchive, it’s easy to use, you can declare a instance and call initialize functions, and then call addFileToZip or UnzipFileTo to finish compression or uncompression.


# Details #

Usage:
Add all the files to you project, and and framework libz.1.2.3.dylib.

include ZipArchive.h using ` #import "ZipArchive/ZipArchive.h" `



To create and add files to a zip

```
		BOOL ret = [zip CreateZipFile2:l_zipfile];
		// OR
		BOOL ret = [zip CreateZipFile2:l_zipfile Password:@"your password"]; //
		//if the Password is empty, will get the same effect as [zip CreateZipFile2:l_zipfile];

		ret = [zip addFileToZip:l_photo newname:@"photo.jpg"];
		if( ![zip CloseZipFile2] )
		{
			// error handler here
		}
		[zip release];

```

Extract files in a zip file to special directory, if the directory does not exist, the class will create it automatically. also if you pass ‘overWrite’ as ‘YES’ it will overwrite files already exist. You can also implement the methods of ZipArchiveDelegate to give more choices for overwriting.

```
	ZipArchive* za = [[ZipArchive alloc] init];
	if( [za UnzipOpenFile:@"/Volumes/data/testfolder/Archive.zip"] )
	// OR
	if( [za UnzipOpenFile:@"/Volumes/data/testfolder/Archive.zip"] Password:@"password of the zip file"] )
  // if the Password is empty, get same  effect as if( [za UnzipOpenFile:@"/Volumes/data/testfolder/Archive.zip"] )
	{
		BOOL ret = [za UnzipFileTo:@"/Volumes/data/testfolder/extract" overWrite:YES];
		if( NO==ret )
		{
			// error handler here
		}
		[za UnzipCloseFile];
	}
 
	[za release];

```