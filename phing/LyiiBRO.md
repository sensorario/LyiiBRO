Come generare il pdf di questa documentazione
---------------------------------------------

Ultimamente tendo a creare sempre della documentazione. In particolare la scrivo
utilizzando il formato reStructuredText. In questo modo posso convertirla in un
pdf con il programma rst2pdf.

Per quanto breve, però, non mi va di lanciare ogni volta il comando

::

    rst2pdf index.rst -o LyiiBRO.pdf

Insieme alla documentazione, tendo ad usare anche phing. Phing si configura
scrivendo un file xml chiamato "build.xml". LyiiBRO utilizza sia phing che
rst2pdf. Ed insieme, vengono utilizzati per generare il pdf completo della
documentazione (LyiiBRO).

::

    <?xml version="1.0" encoding="UTF-8"?>
    <project name="LyiiBRO" default="help">
        <target name="docs">
            <exec command="rst2pdf index.rst -o LyiiBRO.pdf" />
        </target>
        <target name="help">
            <echo>
                LyiiBRO:

                $ phing help        - lancia questo help
                $ phing docs        - genera pdf
            </echo>
        </target>
    </project>

Andando nella directory in cui è stato scaricato LyiiBRO e lanciando il comando

::

    $ phing docs

verrà generato LyiiBRO.pdf.