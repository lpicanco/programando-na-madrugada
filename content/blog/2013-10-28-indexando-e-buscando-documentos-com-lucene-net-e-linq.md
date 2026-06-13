---
title: Indexando e buscando documentos com Lucene.Net e LINQ
date: '2013-10-28T20:57:50Z'
categories:
- .Net
- C#
tags:
- code
- linq
- lucene
---

Código de exemplo:

```csharp
using System;
using System.Linq;
using Microsoft.VisualStudio.TestTools.UnitTesting;
using System.IO;
using Lucene.Net.Store;
using Lucene.Net.Linq;
using Lucene.Net.Linq.Mapping;
using Lucene.Net.Analysis.Standard;

namespace LuceneTests
{
    [TestClass]
    public class LuceneTest
    {
        [TestMethod]
        public void TestIndex()
        {
            // Configura o Lucene.
            var luceneDir = Path.Combine(System.Environment.CurrentDirectory, 
                "lucene_index");

            if (!System.IO.Directory.Exists(luceneDir))
            {
                lock (this)
                {
                    System.IO.Directory.CreateDirectory(luceneDir);
                }
            }

            var directory = FSDirectory.Open(new DirectoryInfo(luceneDir));
            var provider = new LuceneDataProvider(directory, 
                Lucene.Net.Util.Version.LUCENE_30);

            // Indexa os Documentos.
            using (var session = provider.OpenSession<Document>())
            {
                session.Add(new Document()
                {
                    Title = "Hello",
                    Content = "Hello Lucene!"
                });

                session.Add(new Document()
                {
                    Title = "Hi",
                    Content = "Hi, Lucene!"
                });
            }

            // Busca os documentos que contém a palavra "Hello" no título.
            var items = provider.AsQueryable<Document>()
                .Where(l => l.Title.Contains("Hello"));

            Assert.AreNotEqual(items.Count(), 0);
        }
    }
    class Document
    {
        [Field(Analyzer = typeof(StandardAnalyzer))]
        public String Title { get; set; }

        [Field(Analyzer = typeof(StandardAnalyzer))]
        public String Content { get; set; }
    }
}
```
