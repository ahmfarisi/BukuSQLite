Project CRUD SQLite dengan Studi Kasus Sederhana, Data Buku. Menggunakan SQLite Open Helper

Class yang meng-extend SQLite Open Helper untuk kebutuhan CRUD-nya adalah sebagai berikut.

    public class MyDatabaseHelper extends SQLiteOpenHelper {  
	    private Context ctx;  
	    private static final String DATABASE_NAME = "db_buku";  
	    private static final int DATABASE_VERSION = 1;  
	  
	    private static final String TABLE_NAME = "tbl_buku";  
	    private static final String FIELD_ID = "id";  
	    private static final String FIELD_JUDUL = "judul";  
	    private static final String FIELD_PENULIS = "penulis";  
	    private static final String FIELD_TAHUN = "tahun";  
	  
	    public MyDatabaseHelper(@Nullable Context context) {  
	        super(context, DATABASE_NAME, null, DATABASE_VERSION);  
	        this.ctx = context;  
	    }  
  
	    @Override  
		public void onCreate(SQLiteDatabase db) {  
	                  
	        String query = "CREATE TABLE " + TABLE_NAME + " (" +  
	                FIELD_ID + " INTEGER PRIMARY KEY AUTOINCREMENT, " +  
	                FIELD_JUDUL + " TEXT, " +  
	                FIELD_PENULIS + " TEXT, " +  
	                FIELD_TAHUN + " INTEGER ); " ;  
	  
	        db.execSQL(query);  
	    }  
  
	    @Override  
		public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {  
	        db.execSQL("DROP TABLE IF EXISTS " + TABLE_NAME);  
	        onCreate(db);  
	    }  
  
	    public long tambahBuku(String judul, String penulis, int tahun) {  
	        SQLiteDatabase db = this.getWritableDatabase();  
	        ContentValues cv = new ContentValues();  
	  
	        cv.put(FIELD_JUDUL, judul);  
	        cv.put(FIELD_PENULIS, penulis);  
	        cv.put(FIELD_TAHUN, tahun);  
	  
	        long eksekusi = db.insert(TABLE_NAME, null, cv);  
	  
	        return eksekusi;  
	    }  
  
	    public long ubahBuku(String id, String judul, String penulis, int tahun){  
	        SQLiteDatabase db = this.getWritableDatabase();  
	        ContentValues cv = new ContentValues();  
	  
	        cv.put(FIELD_JUDUL, judul);  
	        cv.put(FIELD_PENULIS, penulis);  
	        cv.put(FIELD_TAHUN, tahun);  
	  
	        long eksekusi = db.update(TABLE_NAME, cv, "id = ?", new String[]{id});  
	  
	        return eksekusi;  
	    }  
  
	    public long hapusBuku(String id){  
	        SQLiteDatabase db = this.getWritableDatabase();  
	        ContentValues cv = new ContentValues();  
	  
	        long eksekusi = db.delete(TABLE_NAME, "id = ?", new String[]{id});  
	  
	        return eksekusi;  
	    }  
  
	    public Cursor bacaSemuaData(){  
	        String query = "SELECT * FROM " + TABLE_NAME;  
	        SQLiteDatabase db = this.getReadableDatabase();  
	  
	        Cursor cursor = null;  
	        if(db != null){  
	            cursor = db.rawQuery(query, null);  
	        }  
	  
	        return cursor;  
	    }  
	}

# Video Tutorial

Repositori ini telah dibuat video tutorialnya, bisa di cek pada halaman berikut.

 - **Part 1 :** https://ahmfarisi.com/2021/03/17/record-pengajaran-android-crud-sqlite-part-1-membuat-layout-create-dan-retrieve/
 - **Part 2 :** https://ahmfarisi.com/2021/03/18/record-pengajaran-android-crud-sqlite-part-2-create-dan-retrieve/
 - **Part 3 :** https://ahmfarisi.com/2021/03/23/android-crud-sqlite-part-3-update-dan-delete/
