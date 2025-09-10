Class Item:
//Owning side
@ManyToOne
//@JoinColumn обозначает колонку 'Внешний ключ',
// "person_id" - имя колонки 'Внешний ключ',
// referencedColumnName = "id" - имя колонки в связанной таблице
@JoinColumn(name = "person_id", referencedColumnName = "id")
private Person owner;


Class Person:
//"owner" это название поля в связанной сущности (не таблице!), помеченного как @ManyToOne
@OneToMany(mappedBy = "owner", fetch = FetchType.LAZY)
@Cascade(org.hibernate.annotations.CascadeType.SAVE_UPDATE)
private List<Item> items;
