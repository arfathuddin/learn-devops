# jar

## NAME

jar - Java archive tool

## OPTIONS

- C
  - Temporarily changes directories (cd dir) during execution of the jar command while processing the following inputfiles argument. Its operation is intended to be similar to the -C option of the UNIX tar utility.

- c
  - Creates a new archive file named jarfile (if f is specified) or to standard output (if f and jarfile are omitted). Add to it the files and directories specified by  input files.

- f
  - Specifies the file jarfile to be created (c), updated (u), extracted (x), indexed (i), or viewed (t). The f option and filename jarfile are a pair -- if present, they must both appear.  Omitting f and jarfile accepts a "jar file" from standard input (for x and t) or sends the "jar file" to standard output (for c and u).
- m
  - Includes names and values of attributes from the file specified by the manifest operand in the manifest file of the jar command (located in the archive at META-INF/MANIFEST.MF). The jar command adds the attribute name and value to the JAR file unless an entry already exists with the same name, in which case the jar command updates the value of the attribute. The m option can be used when creating (c) or updating (u) the JAR file.
- u
  - Updates an existing file jarfile (when f is specified) by adding to it files and directories specified by inputfiles
- v
  - Generates verbose output to standard output
- x
  - Extracts  files and  directories from jarfile (if f is specified) or standard input (if f and jarfile are omitted). If inputfiles is specified, only those specified files and directories are extracted. Otherwise, all files and directories are extracted.

## DESCRIPTION

The  jar tool  combines multiple files into a single JAR archive file.  

jar is a general-purpose archiving and compression tool, based on ZIP and the ZLIB compression format.

## EXAMPLES

Typical usage to combine files into a jar file is:

```bash
$ jar cf myFile.jar *.class
.
```

In this example, all the class files in the current directory are placed in the file named myjarfile.  A manifest file entry named META-INF/MANIFEST.MF is automatically generated by the jar tool and is always the first entry in the jar file.  The manifest file is the place where any meta-information about the archive is stored as name:value pairs. Refer to the Jar File specification for details about how meta-information is stored in the manifest file.

If you have a pre-existing manifest file whose name: value pairs you want the jar tool to include for the new jar archive, you can specify it using the m option:

```bash
$ jar cmf myManifestFile myJarFile *.class
.
```

To make jar archive of foo.class with the name as foo.jar

```bash
$ jar uf foo.jar foo.class
.
```

The following would add the file foo.class to the existing jar file foo.jar. The u option can also update the manifest entry, as given by following example which updates the foo.jar manifest with the name: value pairs in manifest.

```bash
$ jar umf manifest foo.jar
.
```

To see the contents of an ear file, you can similarly use

```bash
$ jar -tvf ns-server-ear-xx-3.2.24.0.ear | grep ns-xx-model-3.2.0.0.jar
1390355 Thu Feb 07 11:53:32 +07 2019 lib/ns-xx-model-3.2.0.0.jar
```

To update this with new jar file we can use following

Will replace the jar file lib/ns-ghoperations-model-3.2.0.0.jar in the ear ns-server-ear-tg-3.2.24.0.ear assuming that it is in the directory lib/ in the ear

```bash
$ jar -uvf ns-server-ear-xx-3.2.24.0.ear lib/ns-xx-model-3.2.0.0.jar
updating: ns-xx-model-3.2.0.0.jar (in=1390356) (out=1351630) (deflated 2%)
Total:
------
(in = 62514279) (out = 57862898) (deflated 7%)

$ jar -tvf ns-server-ear-tg-3.2.24.0.ear | grep ns-ghoperations-model-3.2.0.0.jar
1390356 Thu Feb 28 01:25:04 +07 2019 lib/ns-ghoperations-model-3.2.0.0.jar
```

To extract the files from a jar file, use x , as in:

```bash
$ jar xf myFile.jar
.
```

Following would change to the classes directory and add the bar.class from that directory to foo.jar.

```bash
$ jar uf foo.jar -C classes bar.classes
.
```

The following command,
would  change to the classes directory and add to foo.jar all files within the classes directory
(without creating a classes directory in the jar file), then change back to the original directory
before changing to the bin directory to add xyz.class to foo.jar. If classes holds files bar1 and bar2,
then here's what the jar file would contain using jar tf foo.jar:

- META-INF/
- META-INF/MANIFEST.MF
- bar1
- bar2
- Xyz.class

```bash
$ jar uf foo.jar -C classes . -C bin xyz.class
.
```
