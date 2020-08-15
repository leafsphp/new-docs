<!-- markdownlint-disable no-inline-html -->
# Wynter Components <sup><span style="background: rgb(221, 100, 60); color: white; padding: 3px 7px; font-size: 12px;">BETA</span></sup>

Wynter is a full-stack framework built on Leaf that makes building dynamic interfaces simple, without leaving your PHP environment. Wynter is directly implemented from Caleb Porzio's [Livewire](https://laravel-livewire.com).

So basically wynter gives you the power of frontend frameworks, coupled with the full power of PHP. Let's see how this works.

Here's a real-time search component built with Wynter

```php
class SearchUsers extends \Leaf\Wynter\Component {
	public $search;

	public function render() {
		return $this->blade->render("users-search", [
			'users' => $db->select("users", "username", "username LIKE ".$this->search."%")
		]);
	}
}
```
```html
<div>
	<input wynter:model="search" type="text" placeholder="Search Users...">

	<ul>
		@foreach($users as $user)
			<li>{{ $user->username }}</li>
		@endforeach
	</ul>
</div>
```

<br>
Built with ❤ by <a href="https://mychi.netlify.app" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
