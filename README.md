# api documentation for  [sql-cli (v0.4.14)](https://github.com/hasankhan/sql-cli)  [![npm package](https://img.shields.io/npm/v/npmdoc-sql-cli.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-sql-cli) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-sql-cli.svg)](https://travis-ci.org/npmdoc/node-npmdoc-sql-cli)
#### Cross platform command line interface for SQL Server

[![NPM](https://nodei.co/npm/sql-cli.png?downloads=true)](https://www.npmjs.com/package/sql-cli)

[![apidoc](https://npmdoc.github.io/node-npmdoc-sql-cli/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-sql-cli_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-sql-cli/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-sql-cli/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-sql-cli/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Muhammad Hasan Khan"
    },
    "bin": {
        "mssql": "./bin/mssql"
    },
    "bugs": {
        "url": "https://github.com/hasankhan/sql-cli/issues"
    },
    "dependencies": {
        "chardet": "^0.1.0",
        "commander": "^2.9.0",
        "easy-table": "^1.0.0",
        "iconv-lite": "^0.4.13",
        "mssql": "^3.3.0",
        "mstring": "^0.1.2",
        "password-prompt": "^1.0.2",
        "q": "^2.0.3",
        "sprintf-js": "^1.0.3",
        "underscore": "^1.8.3",
        "underscore.string": "^3.3.4",
        "ya-csv": "^0.9.4"
    },
    "description": "Cross platform command line interface for SQL Server",
    "devDependencies": {
        "crlf": "^1.1.0",
        "jasmine-node": "~1.14.3",
        "jshint": "~2.5.1",
        "proxyquire": "~1.0.0"
    },
    "directories": {},
    "dist": {
        "shasum": "3c06e08c6c93ef6e8a3b4df4e7c9e6491efa1c37",
        "tarball": "https://registry.npmjs.org/sql-cli/-/sql-cli-0.4.14.tgz"
    },
    "engines": {
        "node": ">= 4.6"
    },
    "gitHead": "f01e2bdd118e48391202e975ec4df68138af72cf",
    "homepage": "https://github.com/hasankhan/sql-cli",
    "keywords": [
        "node",
        "azure",
        "cli",
        "sql"
    ],
    "licenses": [
        {
            "type": "Apache",
            "url": "http://www.apache.org/licenses/LICENSE-2.0"
        }
    ],
    "main": "./lib/cli.js",
    "maintainers": [
        {
            "name": "hasankhan",
            "email": "hasan@overroot.com"
        }
    ],
    "name": "sql-cli",
    "optionalDependencies": {},
    "preferGlobal": true,
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+ssh://git@github.com/hasankhan/sql-cli.git"
    },
    "scripts": {
        "jshint": "jshint lib",
        "prepublish": "crlf --set=LF bin/mssql",
        "test": "npm -s run-script jshint && npm -s run-script unit",
        "unit": "jasmine-node test"
    },
    "tags": [
        "sql",
        "cli"
    ],
    "version": "0.4.14"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module sql-cli](#apidoc.module.sql-cli)
1.  [function <span class="apidocSignatureSpan">sql-cli.</span>resultwriter (format)](#apidoc.element.sql-cli.resultwriter)

#### [module sql-cli.resultwriter](#apidoc.module.sql-cli.resultwriter)
1.  [function <span class="apidocSignatureSpan">sql-cli.</span>resultwriter (format)](#apidoc.element.sql-cli.resultwriter.resultwriter)
1.  [function <span class="apidocSignatureSpan">sql-cli.resultwriter.</span>CsvWriter ()](#apidoc.element.sql-cli.resultwriter.CsvWriter)
1.  [function <span class="apidocSignatureSpan">sql-cli.resultwriter.</span>JsonWriter ()](#apidoc.element.sql-cli.resultwriter.JsonWriter)
1.  [function <span class="apidocSignatureSpan">sql-cli.resultwriter.</span>TableWriter ()](#apidoc.element.sql-cli.resultwriter.TableWriter)
1.  [function <span class="apidocSignatureSpan">sql-cli.resultwriter.</span>XmlWriter ()](#apidoc.element.sql-cli.resultwriter.XmlWriter)



# <a name="apidoc.module.sql-cli"></a>[module sql-cli](#apidoc.module.sql-cli)

#### <a name="apidoc.element.sql-cli.resultwriter"></a>[function <span class="apidocSignatureSpan">sql-cli.</span>resultwriter (format)](#apidoc.element.sql-cli.resultwriter)
- description and source-code
```javascript
class ResultWriter {
    static create(format) {
        if (!format || format == 't' || format == 'table') {
            return new TableWriter();
        }
        else if (format == 'c' || format == 'csv') {
            return new CsvWriter();
        }
        else if (format == 'x' || format == 'xml') {
            return new XmlWriter();
        }
        else if (format == 'j' || format == 'json') {
            return new JsonWriter();
        }
        else {
            throw new Error(sprintf("Format '%s' is not supported.", format));
        }
    }

    constructor() {
    }

    startResult() {
        this.firstSet = true;
    }

    startSet() {
    }

    writeRows() {
    }

    endSet() {
        this.firstSet = false;
    }

    endResult() {
    }

    formatItem(item) {
        _.each(item, (value, key) => {
            if (value instanceof Date) {
                item[key] = value.toISOString();
            } else if (value instanceof Buffer) {
                item[key] = value.toString('hex');
            }
        });
    }

    log(output) {
        if (output === undefined) {
            output = '';
        }
        console.log(output);
    }
}
```
- example usage
```shell
n/a
```



# <a name="apidoc.module.sql-cli.resultwriter"></a>[module sql-cli.resultwriter](#apidoc.module.sql-cli.resultwriter)

#### <a name="apidoc.element.sql-cli.resultwriter.resultwriter"></a>[function <span class="apidocSignatureSpan">sql-cli.</span>resultwriter (format)](#apidoc.element.sql-cli.resultwriter.resultwriter)
- description and source-code
```javascript
class ResultWriter {
    static create(format) {
        if (!format || format == 't' || format == 'table') {
            return new TableWriter();
        }
        else if (format == 'c' || format == 'csv') {
            return new CsvWriter();
        }
        else if (format == 'x' || format == 'xml') {
            return new XmlWriter();
        }
        else if (format == 'j' || format == 'json') {
            return new JsonWriter();
        }
        else {
            throw new Error(sprintf("Format '%s' is not supported.", format));
        }
    }

    constructor() {
    }

    startResult() {
        this.firstSet = true;
    }

    startSet() {
    }

    writeRows() {
    }

    endSet() {
        this.firstSet = false;
    }

    endResult() {
    }

    formatItem(item) {
        _.each(item, (value, key) => {
            if (value instanceof Date) {
                item[key] = value.toISOString();
            } else if (value instanceof Buffer) {
                item[key] = value.toString('hex');
            }
        });
    }

    log(output) {
        if (output === undefined) {
            output = '';
        }
        console.log(output);
    }
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.sql-cli.resultwriter.CsvWriter"></a>[function <span class="apidocSignatureSpan">sql-cli.resultwriter.</span>CsvWriter ()](#apidoc.element.sql-cli.resultwriter.CsvWriter)
- description and source-code
```javascript
class CsvWriter extends ResultWriter {
    constructor() {
        super();

        this.writer = csv.createCsvStreamWriter(process.stdout);
    }

    startSet() {
        super.startSet();

        if (!this.firstSet) {
            this.log();
        }
        this.firstRow = true;
    }

    writeRows(result) {
        result = result || [];
        result.forEach((item, i) => {
            // if it is first row then write column names
            if (this.firstRow) {
                this.writer.writeRecord(_.keys(item));
                this.firstRow = false;
            }

            this.formatItem(item);

            this.writer.writeRecord(_.values(item));
        });
    }
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.sql-cli.resultwriter.JsonWriter"></a>[function <span class="apidocSignatureSpan">sql-cli.resultwriter.</span>JsonWriter ()](#apidoc.element.sql-cli.resultwriter.JsonWriter)
- description and source-code
```javascript
class JsonWriter extends ResultWriter {
    constructor() {
        super();
    }

    startResult() {
        super.startResult();

        this.log('[');
    }

    startSet() {
        super.startSet();

        if (this.firstSet) {
            this.log('[');
        }
        else {
            this.log(',[');
        }

        this.firstRow = true;
    }

    writeRows(result) {
        var prefix = this.firstRow ? '' : ',';
        this.log(prefix + JSON.stringify(result || [], null, 4));
    }

    endSet() {
        super.endSet();

        this.log(']');
    }

    endResult() {
        super.endResult();

        this.log(']');
    }
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.sql-cli.resultwriter.TableWriter"></a>[function <span class="apidocSignatureSpan">sql-cli.resultwriter.</span>TableWriter ()](#apidoc.element.sql-cli.resultwriter.TableWriter)
- description and source-code
```javascript
class TableWriter extends ResultWriter {
    constructor() {
        super();

        // avoid printing extra blank line after result
        this.appendsLineToResult = true;

        // can afford extra information between resultsets
        this.freeFormat = true;
    }

    startSet() {
        super.startSet();

        if (!this.firstSet) {
            this.log();
        }
    }

    writeRows(result) {
        result.forEach(this.formatItem.bind(this));
        this.log(Table.print(result));
    }
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.sql-cli.resultwriter.XmlWriter"></a>[function <span class="apidocSignatureSpan">sql-cli.resultwriter.</span>XmlWriter ()](#apidoc.element.sql-cli.resultwriter.XmlWriter)
- description and source-code
```javascript
class XmlWriter extends ResultWriter {
    constructor() {
        super();
    }

    startResult() {
        super.startResult();

        this.log('<?xml version="1.0"?>');
        this.log('<results>');
    }

    startSet() {
        super.startSet();

        this.log('   <result>');
    }

    writeRows(result) {
        result = result || [];
        result.forEach(item => {
            this.formatItem(item);

            this.log('       <row>');
            Object.keys(item)
                .forEach(key => {
                    var value = this._escape(item[key]);
                    key = this._escape(key);
                    this.log(sprintf('         <%s>%s</%1$s>', key, value));
                });
            this.log('       </row>');
        });
    }

    endSet() {
        super.endSet();

        this.log('   </result>');
    }

    endResult() {
        super.endResult();

        this.log('</results>');
    }

    _escape(text) {
        if (typeof text !== 'string') {
            return text;
        }

        return text.replace('"', '&quot;')
            .replace("'", '&apos;')
            .replace('<', '&lt;')
            .replace('>', '&gt;')
            .replace('&', '&amp;');
    }
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
