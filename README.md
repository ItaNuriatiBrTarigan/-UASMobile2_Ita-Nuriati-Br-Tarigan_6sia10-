import 'package:flutter/material.dart';

void main() => runApp(MyIta());

class MyIta extends StatelessWidget {
  Widget build(BuildContext context) {
    return MaterialApp(
      routes: {
        "Data": (context) => Ita Nuriati DataTable(),
        "Lupa": (context) => LupaPass(),
        "aritmatika": (context) => Aritmatika(),
      },
      title: 'FORM LOGIN',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Ita Nuriati Br Tarigan (6SIA10)'),
        ),
        body: LoginPage(),
      ),
    );
  }
}

class LoginPage extends StatefulWidget {
  _LoginPageState createState() => new _LoginPageState();
}

class _LoginPageState extends State<LoginPage> {
  final myNirm = TextEditingController();

  String nirm;

  onLogin() {
    nirm = myNirm.text;
    if (nirm == '2018020191') {
      Navigator.pushNamed(context, "Data");
    } else {
      Navigator.pushNamed(context, "Lupa");
    }
  }

  Widget build(BuildContext context) {
    final id = TextFormField(
      keyboardType: TextInputType.emailAddress,
      autofocus: false,
      controller: myNirm,
      decoration: InputDecoration(
        icon: Icon(Icons.person, color: Colors.blue),
        hintText: 'NIRM',
        contentPadding: EdgeInsets.fromLTRB(20.0, 10.0, 20.0, 10.0),
        border: OutlineInputBorder(borderRadius: BorderRadius.circular(32.0)),
      ),
    );

    final loginButton = Padding(
      padding: EdgeInsets.symmetric(vertical: 16.0),
      child: Material(
        borderRadius: BorderRadius.circular(30.0),
        shadowColor: Colors.lightBlueAccent.shade100,
        elevation: 5.0,
        child: MaterialButton(
          minWidth: 200.0,
          height: 42.0,
          onPressed: onLogin,
          // () {Navigator.pushNamed(context, "myApp");},
          color: Colors.lightBlueAccent,
          child: Text('Masuk', style: TextStyle(color: Colors.white)),
        ),
      ),
    );

    return Scaffold(
      backgroundColor: Colors.blue,
      body: Center(
        child: ListView(
          shrinkWrap: true,
          padding: EdgeInsets.only(left: 24.0, right: 24.0),
          children: <Widget>[
            SizedBox(height: 48.0),
            id,
            SizedBox(height: 8.0),
            loginButton,
          ],
        ),
      ),
    );
  }
}

class LupaPass extends StatelessWidget {
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          title: Text('Lupa NIRM'),
        ),
        //body
        body: Text("Nirm Yang Anda Masukkan Salah"));
  }
}

class Ita NuriatiDataTable extends StatefulWidget {
  _Ita NuriatiDataTableState createState() => _Ita NuriatiDataTableState();
}

class _Ita NuriatiDataTableState extends State<Ita NuriatiDataTable> {
  List<DataMahasiswa> barang;

  void initState() {
    super.initState();
    barang = DataMahasiswa.getDataBarang();
  }

  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Ita Nuriati - 2018020191'),
      ),
      body: ListView(children: <Widget>[
        Center(
            child: Text('Data Mahasiswa',
                style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold))),
        DataTable(
          columns: [
            DataColumn(label: Text('')),
            DataColumn(label: Text('')),
          ],
          rows: barang
              .map(
                (barang) => DataRow(cells: [
                  DataCell(Text(barang.id)),
                  DataCell(Text(barang.namabarang)),
                ]),
              )
              .toList(),
        ),
        Padding(
          padding: EdgeInsets.symmetric(vertical: 16.0),
          child: Material(
            borderRadius: BorderRadius.circular(30.0),
            shadowColor: Colors.lightBlueAccent.shade100,
            elevation: 5.0,
            child: MaterialButton(
              minWidth: 200.0,
              height: 42.0,
              onPressed: () {
                Navigator.pushNamed(context, "aritmatika");
              },
              color: Colors.lightBlueAccent,
              child: Text('Program Aritmatika',
                  style: TextStyle(color: Colors.white)),
            ),
          ),
        ),
      ]),
    );
  }
}

class DataMahasiswa {
  //Attribut
  String id;
  String namabarang;

  //Constructor
  DataMahasiswa({this.id, this.namabarang});

  //Data List
  static List<DataMahasiswa> getDataBarang() {
    return <DataMahasiswa>[
      DataMahasiswa(
        id: "Nama",
        namabarang: "Ita Nuriati",
      ),
      DataMahasiswa(
        id: "Jenis Kelamin",
        namabarang: "Perempuan",
      ),
      DataMahasiswa(
        id: "Alamat",
        namabarang: "SiBiru-Biru Ujung Beringin",
      ),
      DataMahasiswa(
        id: "Jurusan",
        namabarang: "Sistem Informasi",
      ),
    ];
  }
}

class Aritmatika extends StatefulWidget {
  _AritmatikaState createState() => new _AritmatikaState();
}

class _AritmatikaState extends State<Aritmatika> {
  final xNama = TextEditingController();
  final xJumlah = TextEditingController();
  final xHarga = TextEditingController();

  String hasil;

  onHitung() {
    setState(() {
      var jumlah = int.parse(xJumlah.text) * int.parse(xHarga.text);
      hasil = "$jumlah";
    });
  }

  Widget build(BuildContext context) {
    final id = TextFormField(
      autofocus: false,
      controller: xNama,
      decoration: InputDecoration(
        hintText: 'Nama',
        contentPadding: EdgeInsets.fromLTRB(20.0, 10.0, 20.0, 10.0),
        border: OutlineInputBorder(borderRadius: BorderRadius.circular(32.0)),
      ),
    );

    final jmlah = TextFormField(
      autofocus: false,
      controller: xJumlah,
      decoration: InputDecoration(
        hintText: 'Jumlah',
        contentPadding: EdgeInsets.fromLTRB(20.0, 10.0, 20.0, 10.0),
        border: OutlineInputBorder(borderRadius: BorderRadius.circular(32.0)),
      ),
    );

    final hrga = TextFormField(
      keyboardType: TextInputType.emailAddress,
      autofocus: false,
      controller: xHarga,
      decoration: InputDecoration(
        hintText: 'Harga',
        contentPadding: EdgeInsets.fromLTRB(20.0, 10.0, 20.0, 10.0),
        border: OutlineInputBorder(borderRadius: BorderRadius.circular(32.0)),
      ),
    );

    final loginButton = Padding(
      padding: EdgeInsets.symmetric(vertical: 16.0),
      child: Material(
        borderRadius: BorderRadius.circular(30.0),
        shadowColor: Colors.lightBlueAccent.shade100,
        elevation: 5.0,
        child: MaterialButton(
          minWidth: 200.0,
          height: 42.0,
          onPressed: onHitung,
          // () {Navigator.pushNamed(context, "myApp");},
          color: Colors.lightBlueAccent,
          child: Text('Hitung', style: TextStyle(color: Colors.white)),
        ),
      ),
    );

    return Scaffold(
      backgroundColor: Colors.white,
      body: Center(
        child: ListView(
          shrinkWrap: true,
          padding: EdgeInsets.only(left: 24.0, right: 24.0),
          children: <Widget>[
            SizedBox(height: 48.0),
            id,
            SizedBox(height: 48.0),
            jmlah,
            SizedBox(height: 48.0),
            hrga,
            SizedBox(height: 8.0),
            loginButton,
          ],
        ),
      ),
    );
  }
}
