# scopeguard

let init_cancelled = scopeguard::guard((), |_| LAYER_IMPL_METRICS.inc_init_cancelled());


# heavier_once_cell

struct LayerInner {
    inner: heavier_once_cell::OnceCell<ResidentOrWantedEvicted>,
}


# Arc::new_cyclic

Use `Arc::new_cyclic` if you want to create a cyclic structure where a Node
references itself or another node that eventually points back to it.

```rust
struct LayerInner {
    // LayerInner internally points to a DownloadedLayer  
    inner: heavier_once_cell::OnceCell<ResidentOrWantedEvicted>,
}

enum ResidentOrWantedEvicted {
    Resident(Arc<DownloadedLayer>),
    WantedEvicted(Weak<DownloadedLayer>, usize),
}

struct DownloadedLayer {
    // and DownloadedLayer points back to the LayerInner
    owner: Weak<LayerInner>,
}
```

See `new_cyclic` function in [this simple demo](https://github.com/winter-loo/snippets-rust/neonlab/src/main.rs).
