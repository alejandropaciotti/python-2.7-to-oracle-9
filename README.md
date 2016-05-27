# python-2.7-to-oracle-9
How to connect to an Oracle database 9 2.7 python

[Download](http://www.oracle.com/technetwork/topics/linuxx86-64soft-092277.html) los siguientes archivos.
oracle-instantclient-basic-11.1.0.1-1.x86_64.rpm
oracle-instantclient-devel-11.1.0.1-1.x86_64.rpm


La herramienta alien es indispensable para convertir los archivos .rpm
a .deb

```shell
sudo apt-get install alien
sudo alien -d *.rpm
```  

Instalación propiamente dicha  

```shell
sudo dpkg -i oracle-instantclient-basic_11.1.0.1-2_amd64.deb
sudo dpkg -i oracle-instantclient-devel_11.1.0.1-2_amd64.deb
```

Crear este archivo:

```shell
 touch /etc/ld.so.conf.d/oracle.conf
```

Escribir en la primer linea:

```shell
/usr/lib/oracle/11.1.0.1/client64/lib/
```

Ejecutar los siguientes comandos:
```shell
$ export ORACLE_HOME=/usr/lib/oracle/11.1.0.1/client64/lib/
$ export LD_LIBRARY_PATH=$ORACLE_HOME/lib
$ sudo ldconfig
```

Si no se bajaron los fuentes bajarlos de [acá](https://pypi.python.org/packages/source/c/cx_Oracle/cx_Oracle-5.1.3.tar.gz#md5=cd6ff16559cbc9c20087ec812c7092ab):

Descomprimirlos y entrar en la carpeta.

```shell
tar -xzvf cx_Oracle-5-1.2.tar.gz
cd cx_Oracle-5-1.2
```

Modificar las lineas del programa setup.py (aprox: 123)

```python
#userOracleHome = os.environ.get("ORACLE_HOME")
 userOracleHome = "/usr/lib/oracle/12.1/client64"
```

Y mas allá:
```python
if oracleHome is None:
       #~ raise DistutilsSetupError("cannot locate an Oracle software " \
               #~ "installation
       oracleHome = "/usr/lib/oracle/11.1.0.1/client64"
```

Luego:
```shell
$ python setup.py build
$ sudo python setup.py install       
```

También instalar libaio-dev

```shell
sudo apt-get install libaio-dev
```


Y listo.

[Fuente](http://www.dangtrinh.com/2014/07/install-cxoracle-513-in-ubuntu-1404.html) principal.
