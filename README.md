import Nat "mo:base/Nat";
import Text "mo:base/Text";
import Bool "mo:base/Bool";
import Result "mo:base/Result";
import Blob "mo:base/Blob";

// actor'e bir isim verebiliyoruz

actor {

  // değişken tanımlama
  // let -> immutable
  // var -> mutable
  // Nat = integer

  var counter: Nat = 0;

  // public fonksiyon tanımla
  public func increment() : async Nat {
    counter += 1;
    counter; // return counter;
  };

  // query fonksiyonu
  public query func get() : async Nat {
    counter;
  };

  // Veri Tipleri
  let number: Nat = 42;
  let text: Text = "Merhaba, Motoko!";
  let boolean: Bool = true;

  // Kompleks tipler
  let array: [Nat] = [1, 2, 3];
  let optional: ?Nat = ?5;

  // Record (Kayıt) Tipi
  type Person = {
    name: Text;
    age: Nat;
  };

  let person: Person = {
    name = "Ali";
    age = 25;
  };

  // Fonksiyonlar ve Asenkron İşlemler 
  public func add(x: Nat, y: Nat) : async Nat {
    x + y;
  };

  public func findValue(arr: [Nat], val: Nat) : async ?Nat {
    for (i in arr.vals()) {
      if (i == val) {
        return ?i; // ?i
      };
    };
    return null;
  };

  // Hata Yönetimi
  public func divide(x: Nat, y: Nat) : async Result.Result<Nat, Text> {
    if (y == 0) {
      return #err("sıfıra bölünemez");
    };
    return #ok(x / y);
  };

  // HTTP istekleri ve Entegrasyon
  public type HttpRequest = {
    method: Text;
    url: Text;
    headers: [(Text, Text)];
    body: Blob;
  };

  public type HttpResponse = {
    status_code: Nat16;
    headers: [(Text, Text)];
    body: Blob;
  };

  public query func http_request(request: HttpRequest) : async HttpResponse {
    {
      status_code = 200;
      headers = [("Content-Type", "text/plain")];
      body = Text.encodeUtf8("Merhaba, Motoko!")
    };
  }

};
